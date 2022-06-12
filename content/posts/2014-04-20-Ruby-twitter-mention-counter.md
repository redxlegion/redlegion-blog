---
comments: true
date: "2014-04-20T21:46:00Z"
categories:
- info
tags:
- ruby
- twitter
- csv
- data
title: Ruby Twitter Mention Counter
---

Ruby is like the Visual Basic of the scripting world. You can do simple
shit in ten lines of code or less. After experimentation, googling, and
satisfaction of curiosity I've sated myself with a simple counterpart to
my python tweet dumper.

Two arguments. Twitter screen name and cutoff for number of mentions.
It's useful to see your data in a new way. I'm going to take it further
pretty soon, processing date information to squeeze every bit of
usefulness out of it.

{{< highlight ruby >}}

require 'csv'

num = ARGV[1].to_i
fil = ARGV[0]

tweets = CSV.read(fil+"_tweets.csv")
tweets = tweets.to_s.scan(/@\w+/)
counts = Hash.new 0
tweets.each { |word| counts[word] += 1 }
lesser = counts.select { |k,v| v > num }.sort_by { |k,v| v }.reverse
lesser = lesser.reject { |k,v| k =~ /#{fil}/ }
lesser.each { |a,b| print "@#{fil}, ",a,", ",b,"\n"  }

{{< / highlight >}}

Output ends up being every mention on the dumped timeline followed by
the number of times it appears. Sorted highest to lowest at cutoff
point. I'm sure it could be useful in "OSINT" crap at a very base level.
In the very least you can stalk your girlfriend/wife and hold it over
her head if you're not the first result. I never had to worry about
that, but it was still fun to peek.
