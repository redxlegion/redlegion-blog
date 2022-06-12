---
comments: true
date: "2012-05-12T11:35:10Z"
tags:
- vpn
- bittorrent
- firewall
- windows
title: Disconnect From P2P if VPN Drops
---

If you're using Windows 7 as a host OS, there's a chance you may need to
occasionally use VPN to cover your ass. VPN services are excellent, but it's an
open-ended technology with a wide variety of possibilities. One of those
unfortunate possibilities is that internet transfers can be resumed if your VPN
connection is dropped for whatever reason. Well, kids, I've got a solution for
you- a Windows 7 native solution at that. I'll use [uTorrent][1] as my example.

1. Open the Network and Sharing center while connected to your VPN provider.
   Ensure that your home wired/wireless connection is set as "Home/Private" and
   the VPN is set as "Public".

   [![VPN Setup](/img/2012/s_vpnsetup1.jpg)](/img/2012/vpnsetup1.jpg)

2. Open "Windows Firewall with Advanced Security".

   [![VPN Setup](/img/2012/s_vpnsetup2.jpg)](/img/2012/vpnsetup2.jpg)

3. Add a new rule for Inbound Connections.

4. Select "Program" for rule type. Choose the path of the program you'd like to
   restrict to VPN only. For action, select "Block the connection". In Profile
   application, check "Domain" and "Private". Leave "Public" unchecked.

   [![VPN Setup](/img/2012/s_vpnsetup3.jpg)](/img/2012/vpnsetup3.jpg)

5. Name your rule, then repeat the steps for Outbound Connections.

Now you're safe against the evils of the MAFIAA. Congratulations. I'm lazy as
hell and didn't feel like screencapping every freaking step, so use your
imagination, play around, learn something new. If you have problems, it's not my
problem, it's your problem.

Today's "Cover Your Ass" tip is brought to you by [this guy](http://practicalrambler.blogspot.se/2011/01/windows-7-firewall-how-to-always-use.html).
Don't get Sabu'd, do this RIGHT NOW.

_**NOTE:** Just want to mention that the rules added by this guide are on a "per
program" basis, which means if you set up these rules selecting 'utorrent.exe',
firefox and other executables will be wholly unaffected if your VPN connection
drops. It's probably possible to sever all connections if VPN drops, though.
Poke around and let me know what you find._

[1]: http://www.utorrent.com/
