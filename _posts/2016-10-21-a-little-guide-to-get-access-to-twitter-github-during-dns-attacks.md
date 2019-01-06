---
layout: post
title:  "A little guide to get access to Twitter, Github during DNS attacks"
date:   2016-10-21 20:00:23 +0700
categories: [experiments]
---

![cover](/static/img/upload/a-little-guide-to-get-access-twitter-github-during-dns-attacks/cover.jpeg?:xl:)

It’s been almost a day now and that seems an eternity for me because i couldn’t get access to my basic vital websites (twitter, github), thanks god i found twitter and github’s ip addresses in my dns cache so i can share them with you.

Basically what the attackers did is they just put down the dns servers so your browser can’t translate twitter.com, github.com to an ip address…but twitter, github and obviously many other website’s servers are still up and running and waiting for their users so here how you can do to get access to them.

**On MacOsX, Linux**

Go to spotlight search, type **terminal** open it

Then type **“sudo nano /etc/hosts”** enter your password

Then add this

```Shell
104.244.42.1 twitter.com
104.244.42.1 twitter.fr
192.30.253.113 github.com
```

Crtl+x then Yes, Enter and you’re done, now you can go again on your browser and check twitter, github 🙂
