---
title: "where are the robots"
subtitle: Web Exploitation
date: 2021-05-03T20:39:35+02:00
tags: ['picoCTF', 'webexploits', 'itsec']
draft: true
---

Can you find the robots? <!--more--> [Link](https://jupiter.challenges.picoctf.org/problem/60915/) or http://jupiter.challenges.picoctf.org:60915

## Writeup
In order to find this flag we need to have a look at the robots.txt ([What Is Robots.txt](https://www.cloudflare.com/learning/bots/what-is-robots.txt/)) file. We can do that by editing the URL by adding **/robots.txt** to the end of the URL. This opens the robots.txt file:
``` html
User-agent: *
Disallow: /8028f.html
```
By adding **/8028f.html** to the end of the original URL, a new site opens on which we can find the flag.

### Flag
picoCTF{ca1cu1at1ng_Mach1n3s_8028f}