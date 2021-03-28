Forensics

# Glory of the Garden
## Description
This [garden](https://jupiter.challenges.picoctf.org/static/d0e1ffb10fc0017c6a82c57900f3ffe3/garden.jpg) contains more than it seems.

## Writeup
Clicking the link prompts you to download the picture 'garden.jpg', which you can open like normal. Having seen that you can hide information in a picture before, I assumed I could try a hexdump of the file:
- `$ xxd > hexdump`
- Looking at the hexdump `$ less hexdump` and searching for the string 'picoCTF' reveals no hit, but searching only for 'CTF' reveals the flag at the bottom of the file
- To out the string, instead of dumping it into a hexfile, we can just use the strings command directly on the image: `$ strings garden.jpg`, which produces the flag at the bottom
- To read out the flag easily, we combine various shell commands:
`$ strings garden.jpg | tail -n 1 | cut -d '"' -f2`

### Flag
picoCTF{more_than_m33ts_the_3y3eBdBd2cc}
<br/>

# So Meta
## Description
Find the flag in this [picture](https://jupiter.challenges.picoctf.org/static/89b371a46702a31aa9931a2a2b12f8bf/pico_img.png).

## Writeup
The link shows you a PNG image. So first things first, downloading the image. Opening the picture named **pico_img.png** with an image viewer works without problems, but also does not give any hint to the flag. So next looking at the title of the challenge, we get an idea what its about: Meta Data.

I recently watched a YouTube playlist about OSINT (Open Source Intelligence), which was quite informative (Link [here](https://www.youtube.com/watch?v=qW96515QG6Y&list=PLrFPX1Vfqk3ehZKSFeb9pVIHqxqrNW8Sy), cudos to Bendobrown for creating the playlist, excelent videos 👍).
One of the [videos](https://youtu.be/d3NsT8lJRlE) explains quite well how to find meta data in images. The suggested tool for this is ExifTool, which we can either download from the creators [homepage](https://exiftool.org/) or on an Ubuntu-Based Linux, its also available via packet manager: `$ sudo apt install exiftool`

After installing ExifTool, we can use it in the command line by entering `$ exiftool pico_img.png`. This will output all the meta data the tool can find in the image. The flag is hidden in the 'Artist' tag. To extract it, we can also use the grep command in combination with ExifTool `$ exiftool pico_img.png | grep picoCTF`.

### Flag
picoCTF{s0_m3ta_eb36bf44}
<br/>

# What Lies Within
## Description
There's something in the [building](https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png). Can you retrieve the flag?

## Writeup
Once again, we start with downloading the file, which is once more a PNG file appropriatly called 'buildings.png'. Opening the file with an image viewer shows us a picture of (presumably) a church. Not much more infos to find with the image viewer. Now we have two ways we can go:
- Looking at the meta data of the picture
- Creating a hexdump and search for the flag within the dump

We start with the meta data. Extracting the data once again with the command line tool 'ExifTool' `$ exiftool buildings.png | grep picoCTF` does not give any result. Therefore, next step will be to produce a hexdump and look for the flag in there.

This time we are going to use the hex editor '**HexEdit**' which we can install with `$ apt install hexedit`. Compared to the built-in `xxd` command, **HexEdit** allows us to switch between the hexadecimal and ASCII view of the file. It also has a built-in search function we can use to look for the flag. Looking at the file with `$ hexedit buildings.png` opens the editor in the terminal window. By pressing **Tab** we can switch between the hex and ASCII view. To use the search function, we press **/** and enter the string we are looking for. Sadly, the flag neither can be found in the hexdump...

So our next best bet is to google possible solution. After searching a bit about 'how to encrypt message in pictures' I come upon an article on [Quora](https://www.quora.com/How-do-I-encrypt-a-message-in-a-image?share=1), describing a process called '**steganography**'. Simply put, with steganography we put an inverted picture with the hidden message 'on top' of another picture. By increasing the transparancy of the picture with the hidden message and layering it with the other picture, we can 'hide' the message within the picture we want the viewer to see.
Looking for a tool online, I come uppon [Steganography Online](https://stylesuxx.github.io/steganography/) where we can upload the picture for decoding. Doing so reveals the hidden message including the flag, hurra 🥳

### Flag
picoCTF{h1d1ng_1n_th3_b1t5}
<br/>

# extensions
## Description
This is a really weird text file [TXT](https://jupiter.challenges.picoctf.org/static/e7e5d188621ee705ceeb0452525412ef/flag.txt)? Can you find the flag?

## Writeup
After downloading the file, first thing we look at it with the shell command `$ file flag.txt`, which promptly reveals that its not what it wants us to think it is. The shell command reveals that the file is not a .txt file at all, instead we got a PNG file. So we can either rename it and change the extensions to the correct file format, or we simply open the file with an image viewer like `$ eog flag.txt`.

Opening the file reveals the flag!

### Flag
picoCTF{now_you_know_about_extensions}
<br/>

# shark on wire 1
## Description
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/483e50268fe7e015c49caf51a69063d0/capture.pcap). Recover the flag.

## Writeup
The downloaded file has the .pcap extension. Looking at it with the file shell command confirms the format - pcap capture file. Looking it up online gives us a further explanation as to what a pcap file exactly is: pcap is an API for capturing network traffic ([Wikipedia](https://en.wikipedia.org/wiki/Pcap)).

The next logic step would be to look up how we can open and analyze such a file. Googling for options to open and analyze the file reveals that we can either look at it with the **tcpdump** shell command or with a GUI Tool called **Wireshark**.

- asdf
- asdf

### Flag
picoCTF{StaT31355_636f6e6e}