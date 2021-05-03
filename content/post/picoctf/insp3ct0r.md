---
title: "Insp3ct0r"
subtitle: Web Exploitation
date: 2021-05-03T20:37:59+02:00
tags: ['picoCTF', 'webexploits', 'itsec']
draft: true
---

Kishor Balan tipped us off that the following code may need inspection:<!--more-->
[Link](https://jupiter.challenges.picoctf.org/problem/44924/) or http://jupiter.challenges.picoctf.org:44924

## Writeup
1) Open Webpage and then Dev Tools in Browser (F12)
2) While looking at the HTML code, we find flag 1/3 in a comment under
   ``` html
   <div id="tababout> [...]
   <!-- Html is neat. Anyways have 1/3 of the flag: picoCTF{tru3_d3 -->
   ```
3) Flag 2/3 can be found as a comment in the stylesheet `mycss.css` (see Style Editor of Dev Tools):
**t3ct1ve_0r_ju5t**
4) Looking at the Debugger Console, we see a JavaScript file `myjs.js`:
   Going through the code, on the bottom there is part 3/3 of the flag: **\_lucky?f10be399}**
   
### Flag
picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?f10be399}