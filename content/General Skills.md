General Skills

# Warmed Up
## Description
What is 0x3D (base 16) in decimal (base 10)?

## Writeup
There are various ways to format a hex value to a decimal value. Here are some:

- Bash: `$ echo $((16#3D))` - **16#** for using Base16, afterwards the hex value (0x implies that its a hex value, but is not part of the actual value)
- Python: either directly in the command line with `$ python3 -c 'print(0x3D)'` or in the python intepreter with the same print function

For outputing the value in the flag format directly, I created a Python program:
```
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
<br/>

# 2Warm
## Description
Can you convert the number 42 (base 10) to binary (base 2)?

## Writeup
Python has a function `bin()` to convert decimal to binary:
- `bin(42) >>> 0b101010` - 0b implies that its a binary number
- `bin(42)[2:] >>> 101010` - with slicing from the second char we can format the result

### Flag
picoCTF{101010}
<br/>

# what's a net cat?
## Description
Using netcat (nc) is going to be pretty important. Can you connect to **jupiter.challenges.picoctf.org** at port **25103** to get the flag?

## Writeup
We can lookup the manual by entering `$ man nc` into the command line. We can assume that the DNS address and port is a server which is listening for any connection on this specific port. Therefore we try and connect to the machine by entering:
`$ nc jupiter.challenges.picoctf.org 25103`

Success! This returns the flag we were looking for.

### Flag
picoCTF{nEtCat_Mast3ry_d0c64587}
<br/>

# strings it
## Description
Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/94d00153b0057d37da225ee79a846c62/strings) without running it?

## Writeup
As we are not allowed to (or at least should not) open the file, we download it into a separate folder. The file has no extension and looking at it with the 'file' command in the shell does not tell as anything more. The name of the challenge does though. It hints to using the shell command 'strings'. Doing so by entering `$ strings strings` prints out a bunch of lines.

As we are looking for a specific string, we can pipe the output into the 'grep' shell command to search for it: `$ strings strings | grep picoCTF` reveals the flag, hurray!

### Flag
picoCTF{5tRIng5_1T_d66c7bb7}
<br/>