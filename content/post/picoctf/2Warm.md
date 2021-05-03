---
title: "2Warm"
subtitle: General Skills
date: 2021-05-03T19:57:47+02:00
tags: ['picoCTF', 'fundamentals', 'itsec']
draft: true
---

Can you convert the number 42 (base 10) to binary (base 2)?

<!--more-->

## Writeup
Python has a function `bin()` to convert decimal to binary:
- `bin(42) >>> 0b101010` - 0b implies that its a binary number
- `bin(42)[2:] >>> 101010` - with slicing from the second char we can format the result

### Flag
picoCTF{101010}