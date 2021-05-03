---
title: "So_Meta"
subtitle: Forensics
date: 2021-05-03T19:28:33+02:00
tags: ['picoCTF', 'forensics', 'itsec']
draft: false
---

Find the flag in this [picture](https://jupiter.challenges.picoctf.org/static/89b371a46702a31aa9931a2a2b12f8bf/pico_img.png).

<!--more-->

![so_meta.png](/img/so_meta.png)

## Writeup
The link opens up a PNG image (the one above). So first things first, downloading the image in order to analyze it. Opening the picture named **pico_img.png** with an image viewer works without problems, but does not give any hint to the flag. But looking at the title of the challenge, we get an idea what its about: Meta Data.

I recently watched a YouTube playlist about OSINT (Open Source Intelligence), which was quite informative (Link [here](https://www.youtube.com/watch?v=qW96515QG6Y&list=PLrFPX1Vfqk3ehZKSFeb9pVIHqxqrNW8Sy), cudos to Bendobrown for creating the playlist, excelent videos 👍).
One of the [videos](https://youtu.be/d3NsT8lJRlE) explains quite well how to find meta data in images. The suggested tool for this is ExifTool, which we can either download from the creators [homepage](https://exiftool.org/) or on an Ubuntu-Based Linux, its also available via packet manager: `$ sudo apt install exiftool`

After installing ExifTool, we can use it in the command line by entering `$ exiftool pico_img.png`. This will output all the meta data the tool can find in the image. The flag is hidden in the 'Artist' tag. To extract it, we can also use the grep command in combination with ExifTool `$ exiftool pico_img.png | grep picoCTF`.

### Flag
picoCTF{s0_m3ta_eb36bf44}