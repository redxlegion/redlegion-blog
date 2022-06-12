---
comments: true
date: "2015-05-21T00:00:00Z"
tags:
- PC-DMIS
- Sentinel
- Dongle
- Security
title: PC-DMIS and Sentinel HASP
---

I recently found myself having to deal with Sentinel HASP and Windows 7.
Specifically, in installing a PC-DMIS version prior to 2013. Windows 7
has this ungainly habit of installing the most recent drivers available
for any piece of equipment plugged into it. This is mostly an alright
thing, but sometimes it creates problems when newer drivers break older
software.

Son of a bitch.

So I attempted to install this older version of PC-DMIS, but it wasn't
communicating at all with the HASP dongle via the new driver. It wasn't
having that at all. I attempted to run `haspdinst.exe -i` to install the
old driver, to no avail. I tried uninstalling the most recent driver
using Device Manager, `haspdinst.exe -remove`, and nothing worked.

It turns out that I'm not the only person who has had to deal with this
damned Sentinel nonsense. The solution is finding this registry entry:

{{< highlight text >}}
HKLM\Software\Aladdin Knowledge Systems\
{{< / highlight >}}

Once you've found it, delete it. Run your older `haspdinst.exe -i`.
Execute `Setup.exe`.

All set.
