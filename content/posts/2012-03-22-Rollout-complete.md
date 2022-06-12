---
categories:
- rant
comments: true
date: "2012-03-22T21:16:00Z"
tags:
- rant
title: Rollout Complete
---

The installation of my virtual soapbox is now complete. I wrote a half-second
bash script to take care of fixing permissions on my end before rsync-ing the
whole load to the "web server" (term used loosely, here, as the janky garbage I
have set up only took two whole seconds of deployment). Everything should be all
set. No more ``XML: PARSER JUST HAD A GODDAMNED FUCKING SEIZURE, YOU RETARD``
style errors or ``403 Asshat Has No Permission`` issues. Should deploy with two
simple commands and let me stand on my little, virtual, audience-less, soapbox
all day long.

Too bad I put all this effort and time into something I have virtually no time
to use! Oh well. I'll figure something out soon, I bet.

Just have to run

	jekyll --server

Check to make sure everything is pretty

	blogsync

This does a call to ``find . -type f -exec chmod 644 {}\;`` and ``-type d`` to
set ``755`` respectively before executing ``rsync`` and sending it all out onto
the tubes. Might suck for a while when uploading music or anything larger than a
few kilobytes, but It'll do.
