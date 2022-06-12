---
comments: true
date: "2013-10-27T13:07:22Z"
tags:
- gr&r
- metrology
- minitab
- gages
title: 'Step by step GR&R with Minitab'
---

I'm going to go through an incredibly quick rundown of how to conduct
your own Gage Repeatability and Reproducibility study using
[Minitab](http://www.minitab.com/). The first thing you should keep in
mind is that there are ways you "should" conduct a GR&R and there are
ways you "shouldn't". You "should" be doing a blind, randomized study
that doesn't allow the "operator" to influence the study with what he
expects. This isn't always the easiest way to begin your first study or
introduce yourself to these types of studies. For your first study, just
do your trials in order.

The first thing you need: three participants. Your three participants do
three trials. You can do more or less, but you need at least two
participants with at least two trials. Next you need ten pieces to
measure. _**CLOCK YOUR PIECES**_. What do I mean? If you're measuring a
circle, mark your circle with a marker as to where it's being measured
on all ten pieces. There are no perfect circles, and if three people
measure ten circles in different ways three times a piece, you're not
going to have collected anything but entropy. Another really, really
important tip: _**You need to have samples to measure at all extremes of
your tolerance**_. If you have ten pieces that are all within a tenth of
a thousandth of an inch of one another and you have a twenty thousandth
of an inch for tolerance, you're going to have an awful GR&R. Your study
variance is going to be enormous and you're not going to have a good
time.

Here is the format for your GR&R worksheet:

|---
|-|1|2|3|4|5|6|7|8|9|10|
|---
|Op1|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|
|Op1|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|
|Op1|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|
|Op2|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|
|Op2|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|
|Op2|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|
|Op3|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|
|Op3|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|
|Op3|10.0|9.0|10.0|8.0|10.0|11.0|10.5|10.1|10.0|10.0|

Once you've collected your data, paste it into Minitab. You'll have to
stack it with this command:

(Enter commands by pressing Ctrl+L.)

{{< highlight text >}}
Stack C6-C15 C3.
{{< / highlight >}}

That takes stacked data from columns C6 to C15 and places it in column
C3.

Next, we'll automagically propagate our data from the table.

{{< highlight text >}}
Set C2
  1( 1 : 10 / 1 )9
  End.
TSet C1
  10(  "Operator 1" "Operator 2" "Operator 3" )3
  End.
{{< / highlight >}}

Those two commands insert part numbers and operator names / trials into
the table as necessary.

Now that we have our data in a format that Minitab likes, we can
continue on to our Nested ANOVA GR&R. Easy command, but you'll have to
edit it to your needs. Change the USL and LSL to the dimension
tolerances of your part.

{{< highlight text >}}
GageRR;
  Parts C2;
  Opers C1;
  Response C3;
  Studyvar 6;
  LSL 8.0;
  USL 11.0.
{{< / highlight >}}

There you have it. The absolute bare necessities to analyze graphically
and statistically the capability of any gage you study. It's incredibly
handy. One of these days I'll write a followup post on how to analyze
the graphs and data output by Minitab. There are other resources out
there, but this is the legwork for getting you going. Nearly anyone can
be a metrologist with this information. Now go, analyze your measurement
equipment!
