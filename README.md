# KentuckyDerbyTweetAnalysis

#Author's Note

The purpose of this project was to give myself something to play with order to learn some basic skills relevant to machine learning.  To that end, I decided to do a variation of a project that had already been done.  In particular, I used Deepna Devkar's project where she analyzes the sentiment of tweets about a basketball game, accessible here: https://github.com/deepnadevkar/twittersentimentanalysis/blob/master/sentimentanalysis_models.ipynb

Here, I analyze tweets about the Kentucky Derby gathered during Derby Day.  You will notice that there are two gaps of several hours in my tweet corpus  (due to some rather silly technical difficulties that I simply didn't know to watch out for!).  Fortunately, I managed to gather tweets during the actual race.  One of the 'learning experiences' I encountered caused me to lose the file I used to gather the tweets.  If you are interested in doing something similar, you can model your code after:
https://github.com/deepnadevkar/twittersentimentanalysis/blob/master/tweetstreaming.py 

So I didn't record what my key tweeted words were (to decide which tweets to collect), other than that I know they included "Kentucky Derby", "Churchill Downs", and several of the front runners' names (but not all contenders).  Because my list of key words was hastily put together before work, take the wordcloud I made with a grain of salt.  However, it did manage to pick up Tom Brady (who attended), despite the fact that I definitely didn't include his name in my key words list.


#Software Used

I did everything in Jupyter Notebook using Python 3.5.  There are many Python modules used in the code, and because the code I modeled from was 2+ years old, I had to change a few parameters and module names here and there.  *Usually* Python error/warning messages are pretty helpful, but sometimes going to StackOver or the documentation was required.


I also want to write a description of how I used mongodb.


I'll write this later: I won't upload sentiment corpus, I will provide a link, though.
http://thinknook.com/twitter-sentiment-analysis-training-corpus-dataset-2012-09-22/ 

# What does this do?
Apparently I have lost the tweet-streaming files, so I can't remember what key words I used...
churchill downs + front-runners, kentucky derby maybe
