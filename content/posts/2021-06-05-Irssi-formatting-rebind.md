---
title: "Irssi Formatting Rebind"
date: 2021-06-05T11:38:03-04:00
draft: false
comments: yes
categories:
- nfo
tags:
- irssi
---

I've been using `irssi` a lot lately to mitigate the sheer volume of networks and channels I dick around in on IRC at any given moment, and using [TheLounge](https://thelounge.chat/) is great and all, but I'm feeding node.js about 3GB just to keep it running. I've noticed that `irssi` barely breaches 130MB of RAM when left to idle. When you combine `irssi` with the really neat tricks like [100 windows in irssi]({{< ref 2012-05-03-100-windows-in-irssi >}}), you can have an extremely RAM-efficient setup that's capable of quick navigation and split-window juggling.

That said, I also want modern convenience, especially all of the formatting capabilities added to IRC itself.

So the first thing I did was set up a prefix keybinding.

```
/bind meta-x key metax
```

So I can start binding things like **bold**:

```
/bind metax-b insert_text \002
```

After that I set up _italics_:

```
/bind metax-n insert_text \029
```

Then I set up <u>underline</u>:

```
/bind metax-m insert_text \030
```

It took me a minute to realize how the prefix worked. It's exactly as it appears. You press Meta-x then b, n, or m, depending on what formatting you're using.

My final setup is now `abduco` -> `dvtm` -> `irssi`, and I have the script `adv_windowlist.pl` outputting my channel activity and list to a FIFO that `dvtm` is reading in a separate pane. It's pretty pimp, ngl.
