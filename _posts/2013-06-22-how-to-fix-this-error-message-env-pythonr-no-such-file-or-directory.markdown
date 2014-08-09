---
author: Thiago Borges
layout: post
title: "How to fix this error message: “env: python\\r: No such file or directory”"
date: 2012-04-16 11:00
comments: true
categories:
  - python
  - django
  - error

---


I was trying to execute `./manage.py` from django framework, and this message was always appearing on my MacOS Lion: “env: python\r: No such file or directory”. I tried to change the first line from manage.py and the only temporary solution was to execute like this: `python manage.py ...` , but it became annoying, I started looking for the solution and I found this solution.

<!--more-->

In a nutshell: it was caused because the break like system of the file is probably from windows (rn), and I need the UNIX system (n)

Fast solution: Open the file with VIM vim file.py , execute this command

`:set fileformat=unix`

and then save and quit with “:x”. I’m not a VIM hardcore expert, neither a VIM user (yet), so take it easy =]

The alternative solution is with dos2unix: I didn’t try this solution because I don’t have dos2unix, but is basically  `dos2unix filename.py`

