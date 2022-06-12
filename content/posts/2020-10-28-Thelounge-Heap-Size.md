---
title: "TheLounge Heap Size"
date: 2020-10-28T11:30:01-04:00
comments: yes
categories:
- software
tags: 
- software
- thelounge
- node
- raspbian
---

Finally I have something technical to contribute. God dammit. So I've decided to embark on a journey of pushing software called `thelounge` to it's breaking point. I'm running it on a raspberry pi 4 with 4GB of RAM and little much else to do except placate me. I set it up to record `-1` lines of buffer and I'm connected to a bouncer that's on multiple networks with a handful of channels on each network. Some are large volume channels with lots of comms.

I knew I'd run into this, but I'm finally experiencing some of the limits of the software. Lately my service has been restarting semi-randomly with a log error as such:

```
Oct 28 11:11:06 raspberrypi thelounge[10187]: FATAL ERROR: Ineffective mark-compacts near heap limit Allocation failed - JavaScript heap out of memory
Oct 28 11:11:06 raspberrypi systemd[1]: thelounge.service: Main process exited, code=killed, status=6/ABRT
Oct 28 11:11:06 raspberrypi systemd[1]: thelounge.service: Failed with result 'signal'.
Oct 28 11:11:11 raspberrypi systemd[1]: thelounge.service: Service RestartSec=5s expired, scheduling restart.
```

Java, JavaScript, and a ton of interpreted or byte compiled languages handle their own garbage collection and typically have rational ceilings set for RAM use. But we're not here to be rational, god dammit. We're here to push shit beyond what it can handle.

After a ton of googling, I found this command line switch for nodejs: `--max-old-space-size=8192`. Thanks, [StackExchange](https://stackoverflow.com/questions/58868373/nodejs-how-do-i-increase-the-memory-heap-size).

But how do I tie this into what I'm doing? Well, Systemd simply points to `/usr/bin/thelounge start` in order to start the process. I opened the file with vim and saw that it's just a typical script using `/usr/bin/env` to execute nodejs for interpretation. I also found you can pass command line arguments with `env`. So I edited the first line of my script just so:

```
#!/usr/bin/env -S node --max-old-space-size=2048
```

Upon restarting `thelounge` I fired up good 'ol `htop` and was greeted with this:

```
10538 thelounge  20   0 1062M  951M 26168 S  0.0 24.9  7:41.20 node --max-old-space-size=2048 /usr/bin/thelounge start
```

Badass. It looks like slipping our little `env` parameter into the binary worked. It'll continue to work until `/usr/bin/thelounge` gets overwritten by an upgrade.
