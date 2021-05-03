---
title: "what's a net cat"
subtitle: General Skills
date: 2021-05-03T19:58:59+02:00
tags: ['picoCTF', 'fundamentals', 'itsec']
draft: true
---

Using netcat (nc) is going to be pretty important. Can you connect to **jupiter.challenges.picoctf.org** at port **25103** to get the flag?

<!--more-->

## Writeup
We can lookup the manual by entering `$ man nc` into the command line. We can assume that the DNS address and port is a server which is listening for any connection on this specific port. Therefore we try and connect to the machine by entering:
`$ nc jupiter.challenges.picoctf.org 25103`

Success! This returns the flag we were looking for.

### Flag
picoCTF{nEtCat_Mast3ry_d0c64587}