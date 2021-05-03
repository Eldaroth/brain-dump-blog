---
title: "shark on wire 1"
subtitle: Forensics
date: 2021-05-03T19:46:00+02:00
tags: ['picoCTF', 'forensics', 'itsec']
draft: true
---

We found this [packet capture](https://jupiter.challenges.picoctf.org/static/483e50268fe7e015c49caf51a69063d0/capture.pcap). Recover the flag.

<!--more-->

## Writeup
The downloaded file has the .pcap extension. Looking at it with the file shell command confirms the format - pcap capture file. Looking it up online gives us a further explanation as to what a pcap file exactly is: pcap is an API for capturing network traffic ([Wikipedia](https://en.wikipedia.org/wiki/Pcap)).

The next logic step would be to look up how we can open and analyze such a file. Googling for options to open and analyze the file reveals that we can either look at it with the **tcpdump** shell command or with a GUI Tool called **Wireshark**.

- asdf
- asdf

### Flag
picoCTF{StaT31355_636f6e6e}