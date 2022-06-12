---
comments: true
date: "2014-05-25T12:46:00Z"
categories:
- info
tags:
- twitter
- ruby
- sqlite
- osint
- Dox the world
title: Twitter OSINT Strategies
---

My current tweet dumper iteration dumps everything collected into a flat
file. That's fine for intermittent use, but won't do much good when we
eventually get into the "big leagues" and start grabbing at streams of
data that will include above and beyond 3200 tweets. Flat files will
quickly swell to sizes that are no longer manageable.

Wat do.

Well, there are hundreds of "database backend" options. Literally
hundreds. We're inevitably going to be storing tweets from various
sources with multiple goals in mind. A veritable forest of `*.csv` files
doesn't neatly organize our data. SQLite3 will provide the backend. It's
local, zero configuration required, and we can concentrate all our
information into a single file with multiple tables.

Compacting a single file and backing it up will make life a great deal
easier. There are also GUI options for taking a peek at information in a
"friendly interface".

Is this the best method? Like I said earlier, there are hundreds of
options. Some strategies work better for other people. It's nothing more
than a choice with no right or wrong answer.

It'll provide me a challenge, along with a few hours of entertainment
when I get free time and don't feel like fragging bullymongs.
