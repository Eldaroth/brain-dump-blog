---
title: Easy1
subtitle: Cryptography
date: 2021-03-12
tags: ['picoCTF', 'cryptography', 'itsec']
draft: false
---

The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help **UFJKXQZQUNB** with the key of **SOLVECRYPTO**. Can you use this table to solve it?

<!--more-->

Table:
```
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 
   +----------------------------------------------------
A | A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
B | B C D E F G H I J K L M N O P Q R S T U V W X Y Z A
C | C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
D | D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
E | E F G H I J K L M N O P Q R S T U V W X Y Z A B C D
F | F G H I J K L M N O P Q R S T U V W X Y Z A B C D E
G | G H I J K L M N O P Q R S T U V W X Y Z A B C D E F
H | H I J K L M N O P Q R S T U V W X Y Z A B C D E F G
I | I J K L M N O P Q R S T U V W X Y Z A B C D E F G H
J | J K L M N O P Q R S T U V W X Y Z A B C D E F G H I
K | K L M N O P Q R S T U V W X Y Z A B C D E F G H I J
L | L M N O P Q R S T U V W X Y Z A B C D E F G H I J K
M | M N O P Q R S T U V W X Y Z A B C D E F G H I J K L
N | N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
O | O P Q R S T U V W X Y Z A B C D E F G H I J K L M N
P | P Q R S T U V W X Y Z A B C D E F G H I J K L M N O
Q | Q R S T U V W X Y Z A B C D E F G H I J K L M N O P
R | R S T U V W X Y Z A B C D E F G H I J K L M N O P Q
S | S T U V W X Y Z A B C D E F G H I J K L M N O P Q R
T | T U V W X Y Z A B C D E F G H I J K L M N O P Q R S
U | U V W X Y Z A B C D E F G H I J K L M N O P Q R S T
V | V W X Y Z A B C D E F G H I J K L M N O P Q R S T U
W | W X Y Z A B C D E F G H I J K L M N O P Q R S T U V
X | X Y Z A B C D E F G H I J K L M N O P Q R S T U V W
Y | Y Z A B C D E F G H I J K L M N O P Q R S T U V W X
Z | Z A B C D E F G H I J K L M N O P Q R S T U V W X Y
```
## Writeup
As I have encountered this type of encryption before, I know this must be a [Vigenère Cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher). We can either solve it by looking for a tool online, or in my case I created a Python script for encrypting and decrypting messages, based on a program I once wrote for CS50 in C.

**vigenere.py**
```
#!/usr/bin/env python3

def shift(char):
    if char.isupper():
        # Shift upper characters
        return (ord(char) - ord('A'))
    else:
        # Shift lower characters
        return (ord(char) - ord('a'))

def encrypt_msg(text, key):
    encrypt_text = []
    counter = 0 # counter for key character to start over if len(text) reached
    for i in range(len(text)):
        if counter == len(key):
            counter = 0

        c = text[i]
        k = key[counter]
        
        if c.isalpha():
            if c.isupper():
                c = ord(c) - ord('A')
                c = ((c + shift(k)) % 26) + ord('A')
            else:
                c = ord(c) - ord('a')
                c = ((c + shift(k)) % 26) + ord('a')
            counter += 1
            encrypt_text.append(chr(c))
        else:
            encrypt_text.append(c)
    return("" . join(encrypt_text))

def decrypt_msg(encrypt_text, key):
    orig_text = []
    counter = 0
    for i in range(len(encrypt_text)):
        if counter == len(key):
            counter = 0
        
        c = encrypt_text[i]
        k = key[counter]

        if c.isalpha():
            if c.isupper():
                c = ord(c) - ord('A')
                c = ((c - shift(k)) % 26) + ord('A')
            else:
                c = ord(c) - ord('a')
                c = ((c - shift(k)) % 26) + ord('a')
            counter += 1
            orig_text.append(chr(c))
        else:
            orig_text.append(c)
    return("" . join(orig_text))

if __name__ == "__main__":
    encrypt = input("Would you like to encrypt a message [Y]/[N]: ").lower()
    if encrypt == 'y':
        text = input("Enter message to encrypt: ")
        key = input("Enter the key: ")
        encrypt_text = encrypt_msg(text, key)
        print("Encrypted message: " + encrypt_text)
    else:
        text = input("Enter message to decrypt: ")
        key = input("Enter the key: ")
        decrypt_text = decrypt_msg(text, key)
        print("Decrypted message: " + decrypt_text)
```

After saving the Python script we can make it executable by using the shell command `$ chmod +x` and execute it simply by typing in `$ ./vigenere.py`.

When executing the script, it prompts you with the question if you'd like to encrypt a message. As we want to decrypt the message, we answer with 'N'. Now we can enter the message which we got in the Description: **UFJKXQZQUNB**, press Enter and then we enter the key **SOLVECRYPTO**. After pressing enter again, it will spit out the decrypted message and voila, we got the flag.
### Flag
picoCTF{CRYPTOISFUN}
