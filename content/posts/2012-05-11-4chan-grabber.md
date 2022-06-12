---
comments: true
date: "2012-05-11T12:58:50Z"
tags:
- 4chan
- ripper
- grabber
- bash
- script
title: 4chan Grabber
---

It's that time again. Time for me to try to sleep and fail miserably. But this
time I only have a three hour window in which to make the attempt, so I'm
considering giving up on the effort entirely. Instead, I'll just post a bash
script that downloads 4chan thread content effortlessly. It's pretty damn handy,
if you think about it. Just execute as such: `4chan <url>`. It was based on
[this script](http://blog.pew.cc/blog/4chan+download+script2/) and modified to
use xargs and concurrent downloads. Without further ado, a quick hack of a quick
hack.

{{< highlight bash >}}
#!/bin/sh

if [ "$1" = "" ]; then
	echo "Usage: `basename $0` <4chan thread url>"
	exit 1
fi

echo "4chan downloader"
echo "Downloading until canceled or 404'd"
LOC=$( echo "$1" | egrep -o '([0-9]*)$' | sed 's/\.html//g' )
echo "Downloading to $LOC"

if [ ! -d $LOC ]; then
	mkdir $LOC
fi

cd $LOC

while [ true ]; do
	TMP=`mktemp /tmp/4chan.XXXXXX`
	TMP2=`mktemp /tmp/4chanm.XXXXXX`
	WGET_CMD='wget -nv -nc'

	wget -O "$TMP" "$1"
	if [ "$?" != "0" ]; then
		rm $TMP $TMP2
		exit 1
	fi

	egrep '//images.4chan.org/[a-z0-9]+/src/([0-9]*).(jpg|png|gif)' "$TMP" -o | uniq > "$TMP2"

        sed 's|//images|http://images|g' $TMP2 > $TMP

        cat $TMP | xargs -P 5 -I _URL_ $WGET_CMD _URL_

	rm $TMP $TMP2
 
	echo "Waiting 30 seconds befor next run"
	sleep 30
done;
{{< / highlight >}}


_**EDIT:** [This guy](http://pastebin.com/FffZVaHu) is a real one-upper. If I
were you, I'd use his insane script._
