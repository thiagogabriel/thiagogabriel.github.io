---
author: Thiago Borges
layout: post
title: "How to install ruby-1.9.3-p194 on rvm"
date: 2012-04-30 23:15
comments: true
categories:
  - ruby
  - error
---

This is the message I received when I tried to install ruby 1.9.3-p194 on RVM:

```
Error running ‘tar xjf /Users/thiago/.rvm/archives/ruby-1.9.3-p194.tar.bz2 -C /Users/thiago/.rvm/tmp/rvm_src_66274 ‘, please read /Users/thiago/.rvm/log/ruby-1.9.3-p194/extract.log
There has been an error while trying to extract the source.
Halting the installation.
There has been an error fetching the ruby interpreter. Halting the installation.
On the log file extract.log was the message:
ruby-1.9.3-p194/ext/tk/sample/demos-jp/spin.rb: (Empty error message)
tar: Error exit delayed from previous errors.
```

<!--more-->

I tried to execute `tar xjf /Users/thiago/.rvm/archives/ruby-1.9.3-p194.tar.bz2 -C /Users/thiago/.rvm/tmp/rvm_src_66274` to be sure it wasn’t a RVM issue and it happened the same problem. This package is broken.

I downloaded another package ruby-1.9.3-p194.tar.bz2 here `~/.rvm/archives/` and executed tried to reinstall rvm `rvm install ruby-1.9.3-p194`

Now every thing happened as expected.