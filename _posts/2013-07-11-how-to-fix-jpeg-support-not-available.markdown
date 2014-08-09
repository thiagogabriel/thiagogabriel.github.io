---
author: Thiago Borges
layout: post
title: "How to Fix: JPEG support not available"
date: 2012-11-27 23:28
comments: true
categories:
  - python
  - Development
  - tip
---


This the most common problem when someone tries to install PIL library on *nix OS. It happens because you don’t have the libraries necessary to handle this kind of format, or you may have but it is not in the right place. This libraries issues are not a python’s fault. It is caused by the system, and you need to install this libraries like [SaltyCrane Blog][salty-blog] or [Jj’s blog][jj-blog] and link to the right location, but it is explained on this articles.

<!--more-->

```bash
---------------------------------------------------------------
    *** TKINTER support not available
    --- JPEG support not available
    --- ZLIB (PNG/ZIP) support not available
    --- FREETYPE2 support not available
    *** LITTLECMS support not available
---------------------------------------------------------------
```

Their solutions solve 90% of the cases, but I need to use PIL in my virtualenv, so I have to make a link from `/usr/lib/`  to `/home/my_user/my_env/lib` . In my case, my libjpeg is named libjpeg.so.62 and I don’t have permission (it is not recommended to rename, because it can be used by other programs). So, I created a link in my virtualenv with other name `ln -s /usr/lib/libjpeg.so.62 /home/my_user/my_env/lib/libjpeg.so`. Just worked on this way.

If you installed PIL with pip, you just have to uninstall and install again. But if you used easy_install I think you have to delete manually. Google it, because I think there are 2 steps to remove easy_install’ed packages.

Let me know if I wasn’t clear enough.

[salty-blog]: http://www.saltycrane.com/blog/2010/10/how-install-pil-ubuntu/
[jj-blog]: http://jj.isgeek.net/2011/09/install-pil-with-jpeg-support-on-ubuntu-oneiric-64bits/