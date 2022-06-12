---
comments: true
date: "2012-05-03T15:11:00Z"
categories:
- irc
tags:
- irssi
- irc
- hardchats
- plagiarism
title: 100 Windows in irssi
---

Life in a terminal can be hard. There are times when a GUI really is useful. "My
kingdom for an Alt+Tab!" IRC can be one of those things. The best coping
mechanism I've found is to google the hell out of any given problem I have until
it's thoroughly solved. Example: Managing a ton of windows in IRC- specifically
irssi. There are terminal clients that do this right off the bat, but irssi is
old and trusted. Without further ado, "100 Windows in irssi", blatantly ripped
off from [this guy](http://niklas.laxstrom.name/page/eng/irssi).

{{< highlight text >}}
/bind meta-q key win1
/bind meta-w key win2
/bind meta-e key win3
/bind meta-r key win4
/bind meta-t key win5
/bind meta-y key win6
/bind meta-u key win7
/bind meta-i key win8
/bind meta-o key win9
/bind meta-p key win0

/bind win0-win0 change_window 00
/bind win0-win1 change_window 01
/bind win0-win2 change_window 02
/bind win0-win3 change_window 03
/bind win0-win4 change_window 04
/bind win0-win5 change_window 05
/bind win0-win6 change_window 06
/bind win0-win7 change_window 07
/bind win0-win8 change_window 08
/bind win0-win9 change_window 09
/bind win1-win0 change_window 10
/bind win1-win1 change_window 11
/bind win1-win2 change_window 12
/bind win1-win3 change_window 13
/bind win1-win4 change_window 14
/bind win1-win5 change_window 15
/bind win1-win6 change_window 16
/bind win1-win7 change_window 17
/bind win1-win8 change_window 18
/bind win1-win9 change_window 19
/bind win2-win0 change_window 20
/bind win2-win1 change_window 21
/bind win2-win2 change_window 22
/bind win2-win3 change_window 23
/bind win2-win4 change_window 24
/bind win2-win5 change_window 25
/bind win2-win6 change_window 26
/bind win2-win7 change_window 27
/bind win2-win8 change_window 28
/bind win2-win9 change_window 29
/bind win3-win0 change_window 30
/bind win3-win1 change_window 31
/bind win3-win2 change_window 32
/bind win3-win3 change_window 33
/bind win3-win4 change_window 34
/bind win3-win5 change_window 35
/bind win3-win6 change_window 36
/bind win3-win7 change_window 37
/bind win3-win8 change_window 38
/bind win3-win9 change_window 39
/bind win4-win0 change_window 40
/bind win4-win1 change_window 41
/bind win4-win2 change_window 42
/bind win4-win3 change_window 43
/bind win4-win4 change_window 44
/bind win4-win5 change_window 45
/bind win4-win6 change_window 46
/bind win4-win7 change_window 47
/bind win4-win8 change_window 48
/bind win4-win9 change_window 49
/bind win5-win0 change_window 50
/bind win5-win1 change_window 51
/bind win5-win2 change_window 52
/bind win5-win3 change_window 53
/bind win5-win4 change_window 54
/bind win5-win5 change_window 55
/bind win5-win6 change_window 56
/bind win5-win7 change_window 57
/bind win5-win8 change_window 58
/bind win5-win9 change_window 59
/bind win6-win0 change_window 60
/bind win6-win1 change_window 61
/bind win6-win2 change_window 62
/bind win6-win3 change_window 63
/bind win6-win4 change_window 64
/bind win6-win5 change_window 65
/bind win6-win6 change_window 66
/bind win6-win7 change_window 67
/bind win6-win8 change_window 68
/bind win6-win9 change_window 69
/bind win7-win0 change_window 70
/bind win7-win1 change_window 71
/bind win7-win2 change_window 72
/bind win7-win3 change_window 73
/bind win7-win4 change_window 74
/bind win7-win5 change_window 75
/bind win7-win6 change_window 76
/bind win7-win7 change_window 77
/bind win7-win8 change_window 78
/bind win7-win9 change_window 79
/bind win8-win0 change_window 80
/bind win8-win1 change_window 81
/bind win8-win2 change_window 82
/bind win8-win3 change_window 83
/bind win8-win4 change_window 84
/bind win8-win5 change_window 85
/bind win8-win6 change_window 86
/bind win8-win7 change_window 87
/bind win8-win8 change_window 88
/bind win8-win9 change_window 89
/bind win9-win0 change_window 90
/bind win9-win1 change_window 91
/bind win9-win2 change_window 92
/bind win9-win3 change_window 93
/bind win9-win4 change_window 94
/bind win9-win5 change_window 95
/bind win9-win6 change_window 96
/bind win9-win7 change_window 97
/bind win9-win8 change_window 98
/bind win9-win9 change_window 99
{{< / highlight >}}
