---
title: "What Lies Within"
subtitle: Forensics
date: 2021-05-03T19:36:20+02:00
tags: ['picoCTF', 'forensics', 'itsec']
draft: false
---

There's something in the [building](https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png). Can you retrieve the flag?

<!--more-->

![what_lies_within.png](/img/what_lies_within.png)

## Writeup
Once again, we start with downloading a file, which is a PNG file appropriatly called 'buildings.png'. Opening the file with an image viewer shows us a picture of (presumably) a church. Not much more infos to find with the image viewer. Now we have two ways we can go:
- Looking at the meta data of the picture
- Creating a hexdump and search for the flag within the dump

We start with the meta data. Extracting the data once again with the command line tool 'ExifTool' `$ exiftool buildings.png | grep picoCTF` does not give any result. Therefore, next step will be to produce a hexdump and look for the flag in there.

This time we are going to use the hex editor '**HexEdit**' which we can install with `$ apt install hexedit`. Compared to the built-in `xxd` command, **HexEdit** allows us to switch between the hexadecimal and ASCII view of the file. It also has a built-in search function we can use to look for the flag. Looking at the file with `$ hexedit buildings.png` opens the editor in the terminal window. By pressing **Tab** we can switch between the hex and ASCII view. To use the search function, we press **/** and enter the string we are looking for. Sadly, the flag neither can be found in the hexdump...

So our next best bet is to google possible solution. After searching a bit about 'how to encrypt message in pictures' I come upon an article on [Quora](https://www.quora.com/How-do-I-encrypt-a-message-in-a-image?share=1), describing a process called '**steganography**'. Simply put, with steganography we put an inverted picture with the hidden message 'on top' of another picture. By increasing the transparancy of the picture with the hidden message and layering it with the other picture, we can 'hide' the message within the picture we want the viewer to see.
Looking for a tool online, I come uppon [Steganography Online](https://stylesuxx.github.io/steganography/) where we can upload the picture for decoding. Doing so reveals the hidden message including the flag, hurra 🥳

### Flag
picoCTF{h1d1ng_1n_th3_b1t5}