---
comments: true
date: "2016-02-28T15:50:00Z"
categories:
- info
tags:
- FreeBSD
- minbif
- IRC
- IM
title: Minbif on FreeBSD
---

I don't remember at all why I did this. I can't remember if the minbif
port was broken or what my motivation was. I downloaded the last
version of minbif and started editing crap until it compiled on
FreeBSD 10.2. Which, with this patch, it does. In any case, it's going
here for posterity, I guess.

{{< highlight diff >}}
diff -Naur minbif-1.0.5/src/im/account.cpp
minbif-1.0.5-new/src/im/account.cpp
--- minbif-1.0.5/src/im/account.cpp     2011-12-04 09:24:51.000000000
-0500
+++ minbif-1.0.5-new/src/im/account.cpp 2016-01-26 17:20:54.418450000
-0500
@@ -272,7 +272,7 @@
                                else
                                {
                                        char** prpl_formats =
g_strsplit(prplinfo->icon_spec.format,",",0);
-                                       ImlibLoadError err =
                                        IMLIB_LOAD_ERROR_UNKNOWN;
+                                       Imlib_Load_Error err =
IMLIB_LOAD_ERROR_UNKNOWN;

                                        close(temp_fd);
                                        /* Try to encode in a
 * supported format. */
diff -Naur minbif-1.0.5/src/im/auth_pam.h
minbif-1.0.5-new/src/im/auth_pam.h
--- minbif-1.0.5/src/im/auth_pam.h      2011-12-04 09:24:51.000000000
-0500
+++ minbif-1.0.5-new/src/im/auth_pam.h  2016-01-26 17:15:57.047434000
-0500
@@ -21,7 +21,7 @@

 #include "auth.h"
 #include <security/pam_appl.h>
-#include <security/pam_misc.h>
+#include <security/openpam.h>

 struct _pam_conv_func_data {
        bool update;
diff -Naur minbif-1.0.5/src/server_poll/daemon_fork.cpp
minbif-1.0.5-new/src/server_poll/daemon_fork.cpp
--- minbif-1.0.5/src/server_poll/daemon_fork.cpp        2011-12-04
09:24:51.000000000 -0500
+++ minbif-1.0.5-new/src/server_poll/daemon_fork.cpp    2016-01-26
12:14:09.049463000 -0500
@@ -20,7 +20,7 @@
 #include <cassert>
 #include <cstring>
 #include <cerrno>
-#include <glib/gmain.h>
+#include <glib.h>
 #include <sys/socket.h>
 #include <sys/stat.h>
 #include <arpa/inet.h>
diff -Naur minbif-1.0.5/src/server_poll/inetd.cpp
minbif-1.0.5-new/src/server_poll/inetd.cpp
--- minbif-1.0.5/src/server_poll/inetd.cpp      2011-12-04
09:24:51.000000000 -0500
+++ minbif-1.0.5-new/src/server_poll/inetd.cpp  2016-01-26
12:09:56.808247000 -0500
@@ -17,7 +17,7 @@
  */

 #include <cassert>
-#include <glib/gmain.h>
+#include <glib.h>

 #include "inetd.h"
 #include "irc/irc.h"
{{< / highlight >}}
