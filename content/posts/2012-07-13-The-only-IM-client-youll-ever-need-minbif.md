---
comments: true
date: "2012-07-13T18:31:00Z"
tags:
- minbif
- intro
- foss
title: 'The only IM client you''ll ever need: Minbif'
---

[Minbif][1] is minimal, flexible, easy to use, and best of all- IRC related.
It's really no more than an IRC interface to libpurple. The biggest difference
between [Bitlbee][2] and minbif is that minbif uses a control scheme very
similar to most popular IRCd's. Bitlbee goes for a "connect via IRC and control
with oddball channel commands" approach. I like minbif's style a great deal more
than bitlbee's.

Here goes.

To compile/install minbif just do the usual:

{{< highlight bash >}}
make ENABLE_TLS=on
make install
{{< / highlight >}}

If you're using FreeBSD like I am, you may or may not have to disable PAM. I
also enabled TLS, as encrypted connections are "A Good Thing&trade;".

To generate certificates for use in minbif, use GnuTLS' built in "certtool".
Place the files wherever you want, but remember the locations of them when it
comes to altering the minbif.conf file.

{{< highlight bash >}}
certtool --generate-privkey --outfile server.key
certtool --generate-self-signed --load-privkey server.key --outfile server.crt
{{< / highlight >}}

Alright. Onto the conf file.

Uncomment the TLS portion (located under irc/daemon) of the conf file as such:

{{< highlight c >}}
                tls {
                        cert_file = /etc/minbif/server.crt
                        key_file = /etc/minbif/server.key
                        priority = PERFORMANCE
                #
                #       # client certificate validation
                #       trust_file = /etc/ssl/certs/ca.crt
                #       crl_file = /etc/ssl/certs/ca.crl
                }
{{< / highlight >}}

We left the trust file commented out, as if it doesn't exist or has issues, it
will prevent minbif from running properly (or at all). Uncomment or add other
options as you require, such as IRCOPs or passwords.

Don't forget to check permissions on your `/var/lib/minbif/users` directory.
Make sure minbif can access it under the user you're running it as.

Now you can start minbif.

{{< highlight bash >}}
minbif /usr/local/etc/minbif/minbif.conf
{{< / highlight >}}

Your minbif.conf location will vary depending on install location. Once it's all
set connect to port 6667 via SSL with your favorite IRC client. You'll be good
to go. Don't forget to connect with a password. The moment you connect with a
password, your account is generated and information saved from that point on.

To start off dicking around with minbif, you can `/quote map help`. That will
kick you off into the excellent world of minbif. Check out the [quick start][3]
as well should you need more help. Enjoy.

[1]: https://symlink.me/projects/minbif/wiki/
[2]: http://www.bitlbee.org/main.php/news.r.html
[3]: https://symlink.me/projects/minbif/wiki/Quick_Start 
