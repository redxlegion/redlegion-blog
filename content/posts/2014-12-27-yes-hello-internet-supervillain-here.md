---
comments: true
date: "2014-12-27T16:28:00Z"
tags:
- doxbin
- tor
- onion
title: '[tor-dev] yes hello, internet supervillain here'
---

Stumbled across this gem from nachash. Interesting read on over two
years of the purest freedom of speech you can find and the effort it
took to maintain.

Good stuff.

{{< highlight text >}}
[tor-dev] yes hello, internet supervillain here

Fears No One nachash at observers.net 
Sat Nov 8 22:10:23 UTC 2014
Previous message: [tor-dev] [PATCH] Pinning middle nodes for HSes:	anti-guard-discovery
Next message: [tor-dev] yes hello, internet supervillain here
Messages sorted by: [ date ] [ thread ] [ subject ] [ author ]

Sorry in advance for the length. I just want to make sure that
everything is included. If you have any questions/clarifications, just
ask. It isn't every day that someone like me pops up on tor-dev, and I
just want to make sure this is as productive and helpful as possible.
This will probably be a very humbling experience, because unlike my
fellow illegal onion operators both past and present, I will actually be
outside of a jail cell and able to read the ruthless dissection of my
set-up. On the bright side, you're all are getting way more info from me
than the pigs will ever willingly cough up, which means if they have
some sort of magic onion decloak trick, this mailing list discussion is
a good chance at finding it. All of these files are in the hands of the
cops anyway (And I have no plans of bringing doxbin back), so there are
0 real-time opsec concerns.

First, the files:

http://doxbin.strangled.net/
http://qhlkmirbijvet2dp.onion/

sha256 and sha512 checksums for all the files are at the bottom.
NOTE: This isn't my box and I didn't set it up.
WARNING: The .xz files will unpack to roughly 1 GB.

Some other info:

1. The box (An OpenVZ VPS) was hosted with Hetzner in Germany. People on
Twitter keep asking if the box was in Bulgaria, but we didn't use
Bulgaria for one simple reason: The very first doxbin box (Bought in
2011) was with a VPS company in Bulgaria. After the first month, they
said "TOR IS ILLEGAL" (I shit you not), killed the box, and kept the $5
we had paid for the 2nd month. Can't say I blame them.

2. It wasn't transproxied. We did this once before, but it became a
hassle to drop iptables rules just to upgrade tor, especially when tor
was getting regular updates semi-recently. Console access with VPS
companies generally requires java plugins or something just as gross, so
there aren't a lot of sane options here. It gets annoying when there's a
surge in the frequency of tor upgrades, so we stopped transproxying the
box. inb4 OMG OPSEC MISTAKE DETECTED!!!11

3. This script (And copypasta that contained its important parts) was
used to build nginx for the various boxes from roughly November 2011 to
mid-October 2014: http://pastebin.com/dBC7E8Jd Early versions didn't use
naxsi, and sed replaced the server banners in the source before
compiling. Yes, I know it doesn't verify the source. See the next point:

4. Around 2 weeks ago, I started grabbing dotdeb.org's source versions
of nginx and building .debs using hardening-wrapper with the following
command at the end:

DEB_CFLAGS_SET="-O2 -fstack-protector-all -fforce-addr -ffast-math
-fomit-frame-pointer -falign-functions=64 -falign-loops=32"
dpkg-buildpackage -uc -us -j8

5. The tor build was from deb.torproject.org. I'm not able to check the
box and never thought to back up /etc/apt/sources, but it used the
experimental-wheezy repo. All updates were done within 24 hours of the
new .debs going live.

6. Last but not least, the elephant in the room: The php is a
headache-inducing nightmare. I inherited the code and it worked, so I
just papered over its defects over the years (There was no anti-flood
protection originally, for example) and built it up to resemble Kowloon
Walled City expressed in php. I have a feeling that a lot of focus is
going to be placed on the code, to the detriment of finding any possible
tor bugs. In any case, everything about doxbin's setup is being
disclosed in the spirit of making this an interesting learning
experience for all parties involved.


BEGIN TINFOIL

Upon scrolling through the .xz files (I personally use xzless), you'll
find a bunch of stuff like:

      1
/%5C%22http://www.hackforums.net/code/fail/code/code/code/code/code/code/old/code/old/code/old/code/code/old/fail/fail/code/fail/fail/fail/fail/fail/fail/code/old/code/old/code/fail/fail/old/old/old/code/code/fail/fail/code/code/fail/old/code/old/old/code/code/fail/code/code/code/old/old/code/code/old/old/old/code/old/fail/fail/old/code/code/old/code/code/code/fail/code/code/code/fail/code/code/fail/fail/old/code/code/code/code/code/code/old/fail/code/code/code/old/code/fail/old/fail/code/code/fail/old/code/fail/fail/code/code/code/code/fail/fail/code/code/old/old/code/code/old/old/old/code/code/old/code/old/code/code/old/old/old/old/code/code/fail/code/old/fail/code/old/code/code/code/code/fail/code/code/code/code/code/code/old/code/code/fail/code/code/code/code/code/code/old/code/fail/fail/fail/code/fail/old/fail/old/fail/old/fail/code/code/fail/fail/fail/code/code/code/fail/code/code/old/code/code/old/fail/fail/code/old/old/fail/old/code/old/old/old/old/old/old/old/pgp.txt

All of the requests were around (If I recall correctly) 3KB in size.
Oddly enough, it caused tor to hiccup pretty badly, although the web
server itself was just fine and I didn't have any network bandwidth
problems (i.e. No obscene traffic spikes). It's also worth pointing out
that the tcp buffers weren't even close to maxed. The same box has
handled a similar volume of legitimate requests before (Namely back in
March, after The Hidden Wiki debacle; see
https://twitter.com/loldoxbin/status/530765088366821377). The solution
to getting tor availability back was to set ConstrainedSockets to 1 and
play with  ConstrainedSockSize (Originally set to 8192, then 4096). This
made doxbin regularly available again, whereas before it was hit or
miss. Once the requests stopped, I waited a couple of days before
commenting those two config lines out and reloaded tor.

A month later, the same kinds of requests started coming in again. After
the first few hours, I started 301 redirecting all requests containing
/%5C%22 to the new Hidden Wiki's Hard Candy page. I also added a grep -v
to my log report script in order to filter out the noise (Possibly a
mistake, but we both tailed logs and watched for something like a
different attack style that the ddos was being used to cover and never
noticed anything). That was good enough to maintain availability, so I
rolled with it and the requests eventually stopped. I have no hard data
on that last point, just the fact that I tailed the access log and the
requests went from 5 per second to 1 every 3-6 seconds before dying off
completely.

I said on Twitter that we suspected it was a deanonymization attempt,
but I didn't elaborate why because LOL 140 CHARACTERS. Intangir (The
other admin, who took over for me from Halloween 2013 to some time
around July of this year) and I talked about it back in August and
decided that an attacker was probably involved spraying specially
crafted packets at the box in order to mess up its circuits, and
eventually get us on attacker-controlled nodes. Since we mitigated the
availability loss, we deemed it as no big deal. In hindsight, that seems
hilariously stupid/naive of us. The kid who started doxbin had a similar
theory that I'm just going to paste verbatim:

<founder> ANYWAY
<founder> i think
<nachash> CONTINUE
<founder> the attack
<founder> was to DoS you
<founder> until you created circuits
<founder> entirely made of dickbleedable nodes
<founder> and then dickbleeding them
<nachash> but the server
<nachash> got seized
<founder> yeah, the IP was discovered by dickbleed though
<founder> the entire circuit was leaking info
<nachash> lol, did you just reproduce this?
<founder> not yet, i'll be trying
<nachash> Do you mind if I share this with tor devs?
<founder> go ahead
<founder> its just a theory at the moment

If either of these theories even remotely pan out, a possible mitigation
for the next person like me (Which shouldn't require any tor dev work)
might look something like this:

1. Make several public relays and configure the torrc of the hidden
service to only make circuits which begin with those nodes. Private
bridges would be a liability in this case because anyone who figures out
the guard node by weaponizing one of attacks from a whitepaper (Which
guard nodes were modded to mitigate) will be able to find the guard node
and then quickly discover that it isn't part of the public tor network.
Public bridges might be ok, but probably less so.
2. Cross your fingers and pray really, really hard that the money trail
is correctly obscured.
3. ????
4. PROFIT! (Or lulz, in my case)

(No, the similarity between the idea of drug market operators giving
back to the network by donating nodes to the practice of drug cartels
building schools and hospitals is not lost on me)

Another thing to consider is the recommendation against running a hidden
service as a relay. Of course, the argument against doing so in the
documentation is very sound. At the same time, the FBI has stated in the
Silk Road criminal complaint that upon finding the IP, the investigator
verified that it wasn't a tor node and knew he had won the onion
lottery. Of course, that could still be psyops/parallel construction
garbage to scare people into making their jobs a little easier, but it's
something to thing about.

END TINFOIL

sha256sums of all the files:

04261115c2ca8d28c439ee16926e271479b8626cc9403d31d686317227f9f4b0
archive.php.txt
2811be83aa41666f245432a1a562a3ac6c7035a59a16beae09571a71723e734c
captcha.php.txt
c5b9bff30748b8d68666f6d4687757f955cde96e67bbb00edad703af45b776ae
doxbin_2014_08_21.txt.xz
cde066ef290ee22c8d78a34af17d33a393845105d21f9fd96db93e0a51290b77
doxbin_2014_08_22.txt.xz
43ec183ee7efc3e9d14d084e50fe054ac6ffb60919e596a8dc4824f116fa1d83
doxbin_2014_08_23.txt.xz
3e630b3843341926ab7667a41a023fa4d63a38d01a5a3549a66f8bc98507cd39
doxbin_2014_08_24.txt.xz
20af2efec930e477fe5595eee66418f87af047ad4316ffc399761002c2d5f45d
doxbin_2014_08_25.txt.xz
1c24eecbc98456a4c2f489a6012a48ec2119927402e7dd1ac12cff7732d04192
doxbin_2014_08_27.txt.xz
afcdafc5293b6a9dbe402da65522f01a231f3f9727a4e597e70cf44321f96c2f
doxbin_php.txt
66d495a5d21df855eedc6e3493a159b2b522b1b8170610c7c7e013f31d01e0ba
doxviewer.php.txt
34611133cb4da451fc45f09e2ca6a08a71267439755b68608cbbc9b2a151ccee
error.php.txt
f37e6be62b149e40fb604cef90313d321f2bf4d2156808ef997a82004307c22f
faq.php.txt
10bc8b38757ad7b27576488a37cec4a2f9dd0ed2ef467cc605ac0da8e83f3e23
index.php.txt
9596d7339f7a89eca7f18dd36cc2f433cdaa23700497816a6a71889158f90bc7
legal.php.txt
912241933303556097d60b890bac18be4577cbefaa6794088b256a3bf1f3796e
naxsi_core.rules.txt
36bfb91a072d43a07de816d78a7cae8b7350a7f8069798468c8f3556acbeab9b
nginx.conf.txt
66df06cdf6e6aba5dab8655e72c30bc5020f2319db1329c2f93bc74e96a96ac4
post.php.txt
b9c12279b289a56702c9a3dc9b873b453ca4642efbcacba597c8bd252a9092ab
privacy.php.txt
728fb96cbecafd974a9afc3211e8d9eb7bbb49f73e3ccb64fe9f7390341b3d38
proscription.php.txt
ae0b124f3ccd849653ef806b10dd41cf316ffd45ef5d8d5af8c2d117027835e4
resources.tar.xz
7ba7ab341f29fc6d5a449bcd2f18c8962b8475b34c8b5745676da4f4c8e51a90
search.php.txt
6aa7c5dbe7aaa25b729ab542e0396f7f7d322244935ea4c0ad0e468b01d19374
thw.php.txt

sha512sum:

7a0e5eaed12d6f7134c56cdd6e68e8255e49c00897fe05701abb84e91d215ed23f462d6b0485467da04a2d7c0a51d5e6a3fece943d9ce2137321a0913448afec
 archive.php.txt
804d679233f811aa66ca6fbc370e0734c7ba830959165496c66a0585637e4c5f966e6dfcbed618bea65ab11aa2f49351840376abc553e74c84001cf5e737da2b
 captcha.php.txt
734adca606f984fce830ebb5d5a05dee0c75d06ff05498483ff057cfd879f670f1a6bd42f5ad090bd63edd0f54d8eed86a0aa04cfe60669c11ac141f271ec366
 doxbin_2014_08_21.txt.xz
c9b55b8b9cf3d3f5820b8cde5b3de77cd609b17c1f6c234118b4b632978a8ef131227500fac66e2238756014437672178515ba028b70f8dc29b0b3b7ef158632
 doxbin_2014_08_22.txt.xz
c63ab075b0383be0703c97bf9fbe42e1dbb3f1ab01eddddbe1752af12bd38a71d6906c2c4c18695b0afa091049ca8583a86b747690cea17c45bd4edcaf269611
 doxbin_2014_08_23.txt.xz
4486fbf61e5132a6167f46c7ec88f7fe25d879e72094d43b3189f786ad84a4e3fd75adc76fddf4ece26b7b670091d29e6a5e7631fd0660b4d549cc49d2e8bcfc
 doxbin_2014_08_24.txt.xz
1ac1e9359092d77e0a13a404ea428cc396b22a8f89dd7bb3241a80a4aa16a3d769aacf0289d1c83e3e367e24ca0a922ca9b3d950a14f962defd6f7c69c62cc63
 doxbin_2014_08_25.txt.xz
e6722d43221a13d6df3f521b040d11a17cd27a63017a73893bf25396468127bbb7f8d81b1b4c7c0aba52e82b09419e63c3df9df877c68fc7603fc9f19b8bda20
 doxbin_2014_08_27.txt.xz
c9d20c82b473260473824ed4909c165f10a3a1a93405cab1ac28d8ae17ee839754998f0d6e7e78c09fec4e21bf4efd6c65ece4734c87f437199cd256cd6756ab
 doxbin_php.txt
b73db1ceefdc501f6ec0fd52c368a88f1e88d80049ed2824fb4a8c60d2c70a87079528f1a043bca6fd2d073ce186eb87531a9cf69b449f537a041786e4f634f3
 doxviewer.php.txt
4f4702f4f4970f67f73b23ca357f764f62eddd63a6fa7878d1c0aeaa2f48ed3813e84261a278ee396aa3e0c6dbe4e5333d8d83b85d173e13be9bea337cf7a678
 error.php.txt
6cfc57fd6f3aaf9a7829b83f8a43852e965dc11929be29f59c494bd8b5723b0fee9aa9ccdc734b8bb07127555d14a8619343061d6fe88508afe7f9ba569ac376
 faq.php.txt
d568388cd9abcad5c0db31a25feef410f7a1a1b26ca3d542b38d1e75c232dbc6d852040dffb3d754d74aac6ecf04e996844b673d4b74ac00c05bb920f63528d1
 index.php.txt
35164a260e89a3ef296460ebfba7b3f5b902b4594fcbc5871e1b431f6c4b89c2e80ae372c50fd6a30d50edeaa94e7326c0cbefca92537e37a3deddbfa610e8f7
 legal.php.txt
93fcbfd36e299239ec2e350fc9a768b9c819089a6922aa997c377d205e7895cd3f6beef00fbadf7de0e02f26efd3ce7a0e47c5d927ae5eb4c9c256c4be58855e
 naxsi_core.rules.txt
1c0ac0e10e715ef8049ea7d1ae3fc635b96a9d62811137e98a4c3794f8ba86f5b66ea883d5ebe939d7cb607cc575e04d8c47ee4ddaabf0887ef44e99c56c4a0a
 nginx.conf.txt
3f29d8d34bc91e1114f089a937bf736b7b74837f5aeb834ae0ace6e7612e2b401bc8f769fa74a432533d92c28b7165eb31dc40eb7ffbfaf82dd870815cc4e189
 post.php.txt
8079dff1ceb2309d98198d3503db8bdaeb38bcdf9679548e8fe7ce1a8bbc87506f8d165713d90c7d2f6316031c1bd7eb7765441d325741c8bd5ca6bc2a6a2843
 privacy.php.txt
a1f6d218a2f65617203d53fbbf625da362d9f2e2676fbc1a28491a1717a6c21367b0a241bd1599c336be2d31d085717b16b3efaffeb383e0a11ce73839ce648f
 proscription.php.txt
94b8bd2fb8b25880e1c25d5fcf60ebe93d3c42857ef61cdf5261dfcaaf1d34cc5d085c358793d22dc7cfd66dcb7628f0eb9953560c3c646d2b7abc08a368c4d3
 resources.tar.xz
0fee75a98e3f8ae4d0c578af399144c49382c7680626cc62e01aa250fad11d1aea522e87ec8e79e6136632bd54bffe681b2ecc283e1d56a7e75b7ab17f7e2319
 search.php.txt
e69bdba3aeb6c94a3b785b96385fafe0ec58e66688333f423004da1a4725bd54666f1e0b427d52068cdbefa430146162f1511c3c0930ea4379f6b022756a48bf
 thw.php.txt

Hope this helps,

- nachash
{{< / highlight >}}
