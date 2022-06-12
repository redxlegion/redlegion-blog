---
comments: true
date: "2014-02-15T00:00:00Z"
tags:
- python
- twitter
- scrape
- tweets
- Dox the world
title: Tweet Scraper in Python
---

Code first, talk later.

{{< highlight python >}}

#!/usr/bin/env python
# encoding: utf-8
 
import tweepy #https://github.com/tweepy/tweepy
import unicodecsv
import sys
 
#Twitter API credentials
consumer_key = ""
consumer_secret = ""
access_key = ""
access_secret = ""
 
 
def get_all_tweets(screen_name):
	#Twitter only allows access to a users most recent 3240 tweets with this method
	
	#authorize twitter, initialize tweepy
	auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
	auth.set_access_token(access_key, access_secret)
	api = tweepy.API(auth)
	
	#initialize a list to hold all the tweepy Tweets
	alltweets = []	
	
	#make initial request for most recent tweets (200 is the maximum allowed count)
	new_tweets = api.user_timeline(screen_name = screen_name,count=200)
	
	#save most recent tweets
	alltweets.extend(new_tweets)
	
	#save the id of the oldest tweet less one
	oldest = alltweets[-1].id - 1
	
	#keep grabbing tweets until there are no tweets left to grab
	while len(new_tweets) > 0:
		print "getting tweets before %s" % (oldest)
		
		#all subsiquent requests use the max_id param to prevent duplicates
		new_tweets = api.user_timeline(screen_name = screen_name,count=200,max_id=oldest)
		
		#save most recent tweets
		alltweets.extend(new_tweets)
		
		#update the id of the oldest tweet less one
		oldest = alltweets[-1].id - 1
		
		print "...%s tweets downloaded so far" % (len(alltweets))
	
	#transform the tweepy tweets into a 2D array that will populate the csv	
	outtweets = [[tweet.id_str, tweet.created_at, tweet.text.encode('utf-8'), tweet.geo, tweet.source] for tweet in alltweets]
	
	#write the csv	
	with open('%s_tweets.csv' % screen_name, 'wb') as f:
		writer = unicodecsv.writer(f)
		writer.writerow(["id","created_at","text","geo","source"])
		writer.writerows(outtweets)
	
	pass
 
 
if __name__ == '__main__':
	#pass in the username of the account you want to download
	get_all_tweets(sys.argv[1])

{{< / highlight >}}

The entirety of this script doesn't belong to me at all. My only
contribution is fixing utf-8 issues. Requires tweepy and unicodecsv.
Outputs tweets in a comma-delimited text file.

...I bet you guys thought I'd post my OAuth tokens. Didn't you? Yeah,
you guys don't think much of me, I know!

Anyway, have fun.

_**Postcript:** I would feel like an ass for posting this snippet without
proper [attribution][1]._

[1]: https://gist.github.com/yanofsky/5436496
