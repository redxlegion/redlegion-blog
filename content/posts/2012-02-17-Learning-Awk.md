---
comments: true
date: "2012-02-17T22:38:00Z"
categories:
- blogging
tags:
- unix
- linux
- awk
- tech
- information
title: Learning Awk
---

One of the most useful little tools for information parsing that I've used has
to be `awk`. Specifically, `awk` will allow you to pipe text through it and use
the `printf()` function to format text as you require it to be formatted. It
also has a basic scripting language that lends further functionality, making it
an ubiquitous tool in the POSIX arsenal. Need to format a list of US States for
a Maruku table? Not a problem. Copy / Paste it into a text file and pipe it
through this: 

{{< highlight bash >}}
awk -F\t ' printf( "%4s | %-20s | %4s", $1, $2, $3) '
{{< / highlight >}}

I'll break that line down for you.  

`-F\t` tells `awk` to separate columns by `[tab]`.  
`printf(` begins the print formatting function.  
`%4s` denotes a string padded with four spaces.  
`|` makes Maruku interpret a table column.  
`%-20s` denotes a left-align string padded up to 20 spaces.  
`$1, $2, $3` tells `printf()` to use the first, second, and third columns.  

It's really pretty easy. The information goes through `stdin()` and exits
`stdout()` as per usual, unless you specify otherwise. I highly recommend
reading more about `awk`, as you'll definitely find a use for it once you do.

**Ratatat / Ratatat - Cherry**  
<object width="400" height="27" data="/swf/audio-player.swf" type="application/x-shockwave-flash">
<param name="bgcolor" value="#ffffff" />
<param name="flashvars" value="playerMode=embedded&amp;audioUrl=/audio/11 Cherry.mp3" />
<param name="wmode" value="window" />
<param name="quality" value="best" />
</object>
