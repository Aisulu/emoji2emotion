## ABOUT

This is a corpus of manually annotated tweets for the emotion detection task (using Plutchik’s eight basic emotions) produced as a result of my master thesis.


## CORPUS FORMAT

Corpus consists of {tweet_id: label} pairs.

**Tweet_id** is an original id of the tweet from Twitter. We can provide only id-s due to Twitter’s policy,  however the way how to get the texts of the tweets will be explained [below](https://github.com/Aisulu/emoji2emotion/blob/master/README.md#corpus-retrieval).

Each **label** represents the emotions in a tweet in form of 8-dimensional vector for 8 emotion types. Each value in a vector is a float number between 0 and 3 representing the presence and intensity of each emotion, where 0 is «absent» and 3 is a «maximum intensity». The emotions in the vector are located in the following order: anger, disgust, fear, joy, sadness, surprise, anticipation, trust.


## CORPUS RETRIEVAL

The [labeled_tweets.txt](labeled_tweets.txt) file contains the corpus in human-readable form.

The [labeled_tweets_dump.txt](labeled_tweets_dump.txt) file contains the corpus in computer readable form. In order to access it, run the following python code:

```
import pickle

labeled_tweets = pickle.load(open('labeled_tweets_dump.txt', 'rb'))

for key in labeled_tweets:
	tweet_id = key
	tweet_label = labeled_tweets[key]
	print(tweet_id, tweet_label)
	
```

To get the text of the tweet using its id:
- install tweepy, create an app and get your credentials
- use following code:
 
```
#set up tweepy

import tweepy

CONSUMER_KEY = #your credentials
CONSUMER_SECRET = #your credentials
ACCESS_TOKEN = #your credentials
ACCESS_TOKEN_SECRET = #your credentials

auth = tweepy.OAuthHandler(CONSUMER_KEY, CONSUMER_SECRET)
auth.set_access_token(ACCESS_TOKEN, ACCESS_TOKEN_SECRET)
api = tweepy.API(auth)

#get the texts

for key in labeled_tweets:
	try:
		tweet_id = key
		tweet = api.get_status(tweet_id)
		print(tweet.text)       
	except:
		print("this tweet does not exist anymore")
```
## CITATION

Please, feel free to use the following BibTex citation if you shall use the corpus for publication purposes:

```
@article{rakhmetullina2018distant,
  title={Distant Supervision for Emotion Classification Task using emoji2emotion},
  author={Rakhmetullina, Aisulu and Trautmann, Dietrich and Groh, Georg},
  url={CEUR-WS.org/Vol-2130/paper6.pdf},
  year={2018}
}
```
