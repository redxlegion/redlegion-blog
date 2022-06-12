---
comments: true
date: "2014-05-22T22:20:00Z"
categories:
- info
tags:
- ruby
- twitter
- scraper
- progressbar
- gem
- Dox the world
title: Ruby Tweet Scraper v.02
---

I've made improvements to the tweet dumper. Added geo information. Also
added progress bar, so check gem requirements.

```ruby
#!/bin/env ruby
# encoding: utf-8

require 'twitter'
require 'csv'
require 'progressbar'

client = Twitter::REST::Client.new do |config|
	config.consumer_key = "YoursHere"
	config.consumer_secret = "YoursHere"
	config.access_token = "YoursHere"
	config.access_token_secret = "YoursHere"
end

scrname = String.new ARGV[0]

def collect_with_max_id(collection=[], max_id=nil, &block)
  response = yield(max_id)
  collection += response
  response.empty? ? collection.flatten : collect_with_max_id(collection, response.last.id - 1, &block)
end

def client.get_all_tweets(user)
  twtcount = user(user).statuses_count
  if twtcount > 3200
      twtcount = 3200 / 200
  else
      twtcount = twtcount / 200
  end
  pbar = ProgressBar.new("Downloading", twtcount)
  collect_with_max_id do |max_id|
    pbar.inc
    options = {:count => 200, :include_rts => true}
    options[:max_id] = max_id unless max_id.nil?
    user_timeline(user, options)
  end
end

junk = client.get_all_tweets(scrname)

CSV.open("#{scrname}.csv", "w") do |csv|
	junk.each do |tweet|
		csv << [tweet.id, tweet.created_at, tweet.user.screen_name, tweet.text, tweet.source, tweet.geo]
	end
end
```

I don't comment. Sorry. I guess I can go back through and comment where
it's helpful and repost another time. It works with Ruby 1.9.2 anyways.

Have phun.

