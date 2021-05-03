---
title: "Extensions"
subtitle: Forensics
date: 2021-05-03T19:40:56+02:00
tags: ['picoCTF', 'forensics', 'itsec']
draft: false
---

This is a really weird text file [TXT](https://jupiter.challenges.picoctf.org/static/e7e5d188621ee705ceeb0452525412ef/flag.txt)? Can you find the flag?

<!--more-->

## Writeup
This one is a relatively short one, especially if you let yourself inspire by the title of the challenge 😉

After downloading the file, first we look at it with the shell command `$ file flag.txt`, which promptly reveals that its not what it wants us to think it is. The shell command reveals that the file is not a '.txt' file at all, instead we got a PNG file. So we can either rename it and change the extensions to the correct file format, or we simply open the file with an image viewer like `$ eog flag.txt`.

Opening the file reveals the flag!

### Flag
picoCTF{now_you_know_about_extensions}
<br/>