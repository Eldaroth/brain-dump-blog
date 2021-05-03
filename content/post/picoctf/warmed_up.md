---
title: "Warmed Up"
subtitle: General Skills
date: 2021-05-03T19:55:28+02:00
tags: ['picoCTF', 'fundamentals', 'itsec']
draft: true
---

What is 0x3D (base 16) in decimal (base 10)?

<!--more-->

## Writeup
There are various ways to format a hex value to a decimal value. Here are some:

- Bash: `$ echo $((16#3D))` - **16#** for using Base16, afterwards the hex value (0x implies that its a hex value, but is not part of the actual value itself)
- Python: either directly in the command line with `$ python3 -c 'print(0x3D)'` or in the python intepreter with the same print function

For outputing the value in the flag format directly, I created a Python program:
``` Python
#!/usr/bin/env python3

def to_base10(hex):
    i = int(hex, 16)
    return str(i)

def to_base16(dec):
    return hex(int(dec))

if __name__ == "__main__":
    choice = input("Would you like to convert to decimal (Base10)? [Y]/[N]: ")
    if choice == 'Y':
        number = input("Please enter number: ")
        print("picoCTF{{{}}}".format(to_base10(number)))
    else:
        number = input("Please enter number: ")
        print("picoCTF{{{}}}".format(to_base16(number)))
```
When executing the program, you get asked if you would like to convert to decimal (from hex) or rather convert decimal to hex.

### Flag
`$ [...]/base16_base10.py` = picoCTF{61}