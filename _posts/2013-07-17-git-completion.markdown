---
layout: post
title: "Git completion"
date: 2013-02-20 23:42
comments: true
categories:
    development
    git
---

Somethings that annoys me is the lack of autocompletion when using command line tools. Everything that makes you more productive should be done, even a shell alias that replaces two commands in one.

Git autocompletion should be add when installed, but it isn’t. (At least not for me.)

<!--more-->

So how can I add autocompletion support to git?
You have to dig into [git source code][git-github] and go to [/contrib/completion][git-github-contrib] path.

The file, in my case (Mac OSX) and usually on Linux, is https://raw.github.com/git/git/master/contrib/completion/git-completion.bash

So what you have to download git-completion script to home directory (it is just a sugestion):

{% highlight bash %}
cd ~
wget https://raw.github.com/git/git/master/contrib/completion/git-completion.bash
{% endhighlight %}

and add the line `source ~/git-completion.bash` to your `~/.bashrc`.

Now you have to reopen your terminal, or run `source ~/git-completion.bash` to reload .bashrc change.

Almost all command line tools have this file, you just have to find the path and do almost the same steps.

[git-github]: https://github.com/git/git
[git-github-contrib]: https://github.com/git/git/tree/master/contrib/completion
