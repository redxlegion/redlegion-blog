---
comments: true
date: "2014-05-21T22:13:00Z"
categories:
- info
tags:
- ruby
- twitter
- OSINT
- Dox the world
title: Ruby Twitter Scraper
---

Requires the twitter gem. Install it as per usual. Code as follows:

```ruby
#!/bin/env ruby
# encoding: utf-8

require 'twitter'
require 'csv'

client = Twitter::REST::Client.new do |config|
	config.consumer_key = "insert"
	config.consumer_secret = "insert"
	config.access_token = "insert"
	config.access_token_secret = "insert"
end

def collect_with_max_id(collection=[], max_id=nil, &block)
  response = yield(max_id)
  collection += response
  response.empty? ? collection.flatten : collect_with_max_id(collection, response.last.id - 1, &block)
end

def client.get_all_tweets(user)
  collect_with_max_id do |max_id|
    options = {:count => 200, :include_rts => true}
    options[:max_id] = max_id unless max_id.nil?
    user_timeline(user, options)
  end
end

junk = client.get_all_tweets(ARGV[0])

CSV.open("#{ARGV[0]}.csv", "w") do |csv|
	junk.each do |tweet|
		csv << [tweet.id, tweet.created_at, tweet.user.screen_name, tweet.text, tweet.source, tweet.geo]
	end
end
```

Excellent. I'm going to revise it as necessary, but it's a most
effective scraper. Though I'd love to add some sort of progress bar to
it, haven't succeeded in that yet. I'll keep you posted and update it as
the iterations of this thing change. It was smashed together from the
twitter gem's bare scraper and CSV output added. I'm quite pleased.
Going to also consider adding time and date statistics compilation. I
might just write an entirely separate script for that. Not sure yet.

More to come.
