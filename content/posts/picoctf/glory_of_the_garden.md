---
title: "Glory of the Garden"
subtitle: Forensics
date: 2021-03-28T13:32:40+02:00
tags: ['picoCTF', 'forensics', 'itsec']
draft: false
---

This [garden](https://jupiter.challenges.picoctf.org/static/d0e1ffb10fc0017c6a82c57900f3ffe3/garden.jpg) contains more than it seems.

<!--more-->

![garden.jpg](/img/garden.jpg)

## Writeup
Clicking the link prompts you to download the picture 'garden.jpg', which you can open like normal. Having seen that you can hide information in a picture before, I assumed I could try a hexdump of the file. Assuming you are using Linux, we can try:
- `$ xxd > hexdump`
- Looking at the hexdump `$ less hexdump` and searching for the string 'picoCTF' reveals no hit, but searching only for 'CTF' reveals the flag at the bottom of the file
- To get the string out, instead of dumping it into a hexfile, we can just use the `strings` command directly on the image: `$ strings garden.jpg`, which produces the flag at the bottom
- To read out the flag easily, we can combine various shell commands:
`$ strings garden.jpg | tail -n 1 | cut -d '"' -f2`

### Flag
picoCTF{more_than_m33ts_the_3y3eBdBd2cc}