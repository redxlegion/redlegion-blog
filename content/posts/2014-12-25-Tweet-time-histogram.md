---
comments: true
date: "2014-12-25T21:01:00Z"
tags:
- OSINT
- cyberstalking
- ruby
- minitab
- Dox the world
title: Tweet Time Histogram
---

I've figured out an easy way to get at interesting data. First I fire up
the tweet nabber written in ruby, then run this cheap piece of crap and
extract only time data from tweets pulled.

After getting the time data, I open the \*.csv in Minitab and create a
histogram with it. I then have the frequency with which a person tweets
over 3k tweets by time, so I can approximate when they're most active
throughout the day based on my relative time zone.

Awesome.

I hope to figure out more interesting ways to analyze data to garner
information like this.

{{< highlight ruby >}}
require 'csv'
require 'time'
require 'tzinfo'

fil = ARGV[0]
stuff = Array.new

tweets = CSV.read(fil)
tweets.each do |x|
	if x[1] != "created_at" and x[3].start_with?("RT @") == false then
		times = Time.parse(x[1].to_s)
		shift = times.getlocal("-05:00")
		stuff << "#{shift.hour}:#{shift.min}:#{shift.sec}"
	end
end
puts stuff
{{< / highlight >}}

So basically:

1. Fire up [tweet scraper]({{< ref 2014-05-22-Ruby-tweet-scraper-v02 >}}).
2. Parse CSV with this script.
3. Import (HH:MM:SS) in Minitab and get a histogram like this:

![Minitab Histogram](/img/2014/histogram_of_times.jpg)

Simple.

_**Note:**_ I've edited this thing like eighty times. This last
iteration filters retweets out, since I'm pretty sure we don't need that
polluting our data. Now you should have pure origin tweets to discern
when people are most active. Shift your time zone accordingly, and I'm
sure you'll be able to effectively stalk twitter users in no time!
DOXDOXDOXDOXDOXDOX
