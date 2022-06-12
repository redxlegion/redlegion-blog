---
comments: true
date: "2015-01-09T18:53:00Z"
categories:
- info
tags:
- ping
- rant
- infosec
- histograms
- excel
- microsoft
- office
title: Ping / Cheap Histograms
---

Living. That's what I've been busy with. But I think I'm going to share
a tidbit of knowledge to the poor kids out there who either aren't smart
enough to pirate a copy of Minitab or aren't fortunate enough to drop
$1500 on statistical analysis software. I'm going to show you how to do
binning with Excel (and potentially LibreOffice / OpenOffice).

Excel binning is the easiest. It's also a great deal more flexible than
Minitab.

First, you have to highlight a range of cells that you wish to turn into
a histogram. Lets say `A1:A5` is your series of bin values. We could
easily say:

|A|
|-|
|12:00|
|13:00|
|14:00|
|15:00|
|16:00|

Is your table for binning. Now if you select `B1:B5` and press `F2`, you
can type in `=FREQUENCY(DataRange,A1:A5)` and then press
`Ctrl+Shift+Enter`. You'll end up with:

|A|B|
|-|-:|
|12:00|0|
|13:00|13|
|14:00|28|
|15:00|8|
|16:00|32|

And it will depend on the data you select, what you'll end up seeing as
a histogram.

This actually is a great way to analyze information collected with my
prior script located at <a href="{{< ref 2014-12-25-Tweet-time-histogram >}}">this url</a>.

Don't forget, you're going to need a range of data to process for
`DataRange`. A most likely candidate would be something like:

|D|
|-|
|12:31|
|12:45|
|12:51|
|12:51|
|etc.|

Excel's "Frequency" function just counts the number of matches between
bins, which it will also do with time or date data as applicable,
especially in the aforementioned "tweet time histogram" blog post. Good
stuff.

Have fun processing data!

Oh. Yeah, I guess I could try to figure the LibreOffice/OpenOffice
equivalents out, but I think I'll leave that to you.

Get to it, infosec freak! Remember, you have to SELECT THE RANGE you
wish to propagate with histogram data FIRST, then you have to press `F2`
and enter the formula as I stated earlier. Shit is important, otherwise
it won't work. So yeah. "Teach a man to fish" and all that.
