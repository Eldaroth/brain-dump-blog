---
title: "strings it"
subtitle: General Skills
date: 2021-05-03T19:59:57+02:00
tags: ['picoCTF', 'fundamentals', 'itsec']
draft: true
---

Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/94d00153b0057d37da225ee79a846c62/strings) without running it?

<!--more-->

## Writeup
As we are not allowed to (or at least should not) open the file, we download it into a separate folder. The file has no extension and looking at it with the 'file' command in the shell does not tell us anything more. The name of the challenge does though. It hints to using the shell command 'strings'. Doing so by entering `$ strings strings` prints out a bunch of lines.

As we are looking for a specific string, we can pipe the output into the 'grep' shell command to search for it: `$ strings strings | grep picoCTF` reveals the flag, hurray!

### Flag
picoCTF{5tRIng5_1T_d66c7bb7}