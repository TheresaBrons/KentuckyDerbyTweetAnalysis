# KentuckyDerbyTweetAnalysis

In my first project, I analyze the sentiment of tweets about the Kentucky Derby gathered during Derby Day (keeping it light during the big health care debate!). 

# Purpose of Project & Disclaimer

The purpose of this project was to give myself something to play with order to learn some basic skills relevant to machine learning.  To that end, I decided to do a variation of a project that had already been done.  In particular, as a model, I used Deepna Devkar's project where she analyzes the sentiment of tweets about a basketball game, accessible here:  https://github.com/deepnadevkar/twittersentimentanalysis/blob/master/sentimentanalysis_models.ipynb and here: http://www.nbalogic.com/nbadetail_C2cF5H7jA0F5j.htm

Since the code I was customizing is 2+ years old, I got a lot of warnings/errors due to changes in the packages used (or even changes I made to the code).  Fortunately, Python error/warning messages are *usually* pretty helpful.  But thank heavens for StackOverflow!

You will notice that there are two gaps of several hours in my tweet corpus  (due to some rather silly technical difficulties that I simply didn't know to watch out for!).  Fortunately, I managed to gather tweets during the actual race.  Later, one of the, shall we say 'learning experiences' I encountered caused me to lose the code I used to gather the tweets.   I customized the following code to gather the streaming data:
https://github.com/deepnadevkar/twittersentimentanalysis/blob/master/tweetstreaming.py   

One point is, though, that I don't have a record what my key words were (to decide which tweets to collect), other than that I know they included "Kentucky Derby", "Churchill Downs", and several of the front runners' names (but not all contenders).  Because my list of key words was hastily put together before work, take the wordcloud I made with a grain of salt.  However, it did manage to pick up Tom Brady (an attendee, not a contender, silly), despite the fact that I definitely didn't include his name in my key words list.  

# Software Used

To gather tweets, you need to make a twitter developer account to access the Twitter API.  For those interested, here's a tutorial: https://www.dataquest.io/blog/streaming-data-python/ 

I did almost everything in Jupyter Notebook using Python 3.5.  I used MongoDB, Tweepy, and Pymongo to get the tweets into a JSON file. After that, I manipulated and plotted the data with the help of several Python packages (see code).  

# Twitter Sentiment Corpus

To train my machine learning algorithms to guess the sentiment value of the tweets I gathered, I used the Twitter Sentiment Analysis Dataset, which at the time held more than 1.5 million tweets.  Amazingly, all of them have been evaluated for their sentiment value: 1 for positive and 0 for negative.  You can find a link here: 
http://thinknook.com/twitter-sentiment-analysis-training-corpus-dataset-2012-09-22/ 

The file is enormous, so I isolated about 100,000 of them for use.  Code for that: https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/MakeMiniCorpus.ipynb 

I Devkar's code to read and clean the mini-corpus, preparing it for the algorithms: https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/ReadAndCleanMiniCorpus.ipynb

# Kentucky Derby Corpus

The first thing I noticed upon inspecting the JSON file (as a PANDAS dataframe) was that I had a fair number of Portuguese tweets!  Whoops, it turns out that the Derby Paulista, a 100 year old soccer rivalry between the Corinthians and the Palmeiras, who have a match every year in Sao Paulo, Brazil, is still hot topic of conversation.  So I used TextBlob to collect only the English tweets in the hopes that most people speaking English would be talking about the Kentucky Derby.

I learned right away that TextBlob relies on Google Translate.  In other words, it needs a good internet connection!  The code took about 5 hours to run after I finally got a stable internet connection.  I've since played with it, so you can't see the output anymore, but here's what I ran:
https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/Kentucky%20DerbyEnglish.ipynb

You'll notice that the code also cleans up the text of the tweets to prepare them for the analysis algorithms.  You can see the output in: https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_cleantext.csv

# Derby Data Visualization
In https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/DerbyDataVisualizations.ipynb I create two images.

The first is one of those famous 'wordclouds'.  The text colors are random (the wordcloud is generated before any sentiment analysis), but the size of the word is correlated with its frequency in the Derby tweet corpus.  Here is the link:
![alt text](https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/twitter_derby.png)


The frequency of the 25 most commonly tweeted words in the Derby tweet corpus.  I'm a little surprised 'one' isn't considered a stopw![alt text](ord (stopwords are words that are considered to have little information about sentiment and that are removed from tweets during the 'cleaning' process).  But, surprising to me, 'co' deserves to be up there; a "co-favorite" happened to be the winner of the Derby this year!
![alt text](https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_frequency_distr.png)

<img src="https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_frequency_distr.png" width="1200" height="840">


# Training Sentiment Analysis Algorithms

For reference (and some cool graphs), see:
https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/TrainSentimentAnalysis.ipynb

To begin, after separating the tweets into training and testing tweets (a 90/10 split), the cleaned tweets have to be transformed into a format that the machine learning algorithms can understand.  That's where TfidfVectorizer.fit_transform() comes in handy.  It turns each tweet into a numpy.ndarray containing 5000 numbers.  Each entry in an refers to a particular word in TfidfVectorizer's 5000 word dictionary, and if that particular word shows up in a given tweet, that tweets array will have a non-zero number in that place (bigger if the word is less common).  Now we have a 'bag of words'.

Once the Derby training tweets are represented by a (number of tweets)x(5000) array, they're fed into 3 different machine learning algorithms: Random Forests (through scikit's RandomForestClassifier), multinomial Naive Bayes, and the Support Vector Machine.  For each of these, I've printed out the "confusion matrix", which shows how well each algorithm did at guessing the sentiment of the test data.  Rows indicate the actual classification of tweets (top row negative tweets, bottom row for positive tweets), and columns indicate what the given algorithm guessed the sentiment was.  

The precision, recall, and f1 scores are also reported.  To interpret the result, look at the first row of one of the reports (the row concerning negative tweets):
* Precision: Of the tweets guessed to be negative, what proportion are actually negative?
* Recall: Of the tweets that are actually negative, what proportion were guessed to be negative?
* f1 score: weighted average of the precision and recall, 1 means algorithm is perfect

The algorithms perform pretty similarly, but the Naive Bayes was more balanced between precision and recall for both types of tweets, so I used that algorithm to analyze the Derby tweet corpus.

Here are the results:
![alt text](https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_posNeg.png)

Later, I used Textblob's sentiment.polarity to get a sense of how positive and negative tweets.  The bar graph below shows that most tweets were relatively neutral.
![alt text](https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_posNegNeut.png)
![alt text](https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_sentdistr.png)


# Derby Tweet Stats Over Time

The following code produces some interesting graphs, described below.  The statistical analysis had to be done with a pandas.core.series.Series of pandas.libs.tslib.Timestamp objects. But to graph, I wanted a list of just the times, adjusting for some bizarre time-zone issue that I will never be able to figure out, having permanently lost the file I used to stream.  So you'll see a little work-around that Devkar didn't have to do.
https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/DerbyTweetStatsOverTime.ipynb

The first graph it produces shows the 1 minute tweet count totals, graphed over time.  No, people did not suddenly stop tweeting during two periods of Derby Day.  Instead, my computer suffered some technical difficulties during the tweet streaming due to operator error - funny story!  Oh, live and learn... 
https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_tweet_counts.png

The link below shows the plot of the 5m averages of sentiment polarity over time.  The vertical gray line indicates time period from 6:55-7:00pm, which is the 5 minute period when tweeting activity was most intense (about 10 minutes after the race itself). 
https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_sentimentPolarity_vs_time.png



