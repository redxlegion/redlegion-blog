---
comments: true
date: "2012-03-22T19:36:05Z"
categories:
- blogging
tags:
- info
- jekyll
title: New Jekyll Setup
---

My prior [Jekyll][] setup was as such:

1. Jekyll installed on [Amazon EC2][] instance.
2. Template/files generated on EC2 instance.
3. Uploaded content to template/work directory as needed.

I've since decided that was "A Bad Idea&trade;", and have chosen to offload the
work from the EC2 instance to my [FreeBSD][] machine instead, updating content with
rysnc as it's generated. This poses a few minor annoyances for the moment.
First, the DSL I'm connected to is currently crawling at a snail's pace.
However, the nice thing is that you, the reader, don't see all my ugly fuckups
as they happen. Instead, you only get to see the pretty pre-formatted pages as
they're ready for print. That's a major advantage. As I learn [Maruku][], you're
not forced to watch me painfully learn it's syntax. Good stuff, huh?

Well, that's it for an update today. I know, it sucks, but it's not like I have
all the time in the world to [just blog all day][].

**UPDATE:** I really suck at file permissions. You may or may not notice a lot
of 403 errors. Go ahead and ignore those, I'll figure this out eventually.

**MOAR UPDATE:** I think I'm retarded. Thatisall. Also, I love [rsync][]. It's the
best thing since sliced bread.

[Jekyll]: https://github.com/mojombo/jekyll
[Amazon EC2]: http://aws.amazon.com/ec2/
[FreeBSD]: http://www.freebsd.org/
[Maruku]: http://maruku.rubyforge.org/maruku.html
[just blog all day]: {{< ref 2012-02-18-Blogging-all-damn-day >}}
[rsync]: http://rsync.samba.org/
