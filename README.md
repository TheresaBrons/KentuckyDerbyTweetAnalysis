# KentuckyDerbyTweetAnalysis

In my first project, I analyze the sentiment of tweets about the Kentucky Derby gathered during Derby Day (keeping it light during the big health care debate!). 

# Purpose of Project & Disclaimer

The purpose of this project was to give myself something to play with order to learn some basic skills relevant to machine learning.  To that end, I decided to do a variation of a project that had already been done.  In particular, as a model, I used Deepna Devkar's project where she analyzes the sentiment of tweets about a basketball game, accessible here:  https://github.com/deepnadevkar/twittersentimentanalysis/blob/master/sentimentanalysis_models.ipynb and here: http://www.nbalogic.com/nbadetail_C2cF5H7jA0F5j.htm

Since the code I was customizing is 2+ years old, I got a lot of warnings/errors due to changes in the packages used (or even changes I made to the code).  Fortunately, Python error/warning messages are *usually* pretty helpful.  But thank heavens for StackOverflow!

You will notice that there are two gaps of several hours in my tweet corpus  (due to some rather silly technical difficulties that I simply didn't know to watch out for!).  Fortunately, I managed to gather tweets during the actual race.  One of the 'learning experiences' I encountered caused me to lose the code I used to gather the tweets.   I customized the following code to gather the streaming data:
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

The first is one of those famous 'wordclouds'.  The text colors are random (the wordcloud is generated before any sentiment analysis), but the size of the word is correlated with its frequency in the Derby tweet corpus.  Here is the link: https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/twitter_derby.png

The frequency of the 25 most commonly tweeted words in the Derby tweet corpus.  I'm a little surprised 'one' isn't considered a stopword (stopwords are words that are considered to have little information about sentiment and that are removed from tweets during the 'cleaning' process).  But, surprising to me, 'co' deserves to be up there; a "co-favorite" happened to be the winner of the Derby this year!
https://github.com/TheresaBrons/KentuckyDerbyTweetAnalysis/blob/master/derby_frequency_distr.png


# Training Sentiment Analysis Algorithms
