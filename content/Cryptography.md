Cryptography

# Easy1
## Description
The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help **UFJKXQZQUNB** with the key of **SOLVECRYPTO**. Can you use this table to solve it?

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
Created a Python program for encrypting and decrypting messages, based on a program I wrote in C for CS50 (on GitHub).

```
#!/usr/bin/env python3

def shift(char):
    if char.isupper():
        # Shift upper characters
        return (ord(char) - ord('A'))
    else:
        # Shift lower characters
        return (ord(char) - ord('a'))

def encrypt(string, key):
    encrypt_text = []
    counter = 0 # counter for key character to start over if len(string) reached
    for i in range(len(string)):
        if counter == len(key):
            counter = 0

        c = string[i]
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

def decrypt(encrypt_text, key):
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
    encrypt = input("Would you like to encrypt a message [Y]/[N]: ")
    if encrypt == 'Y':
        string = input("Enter message to encrypt: ")
        key = input("Enter the key: ")
        encrypt_text = encrypt(string, key)
        print("Encrypted message: " + encrypt_text)
    else:
        string = input("Enter message to decrypt: ")
        key = input("Enter the key: ")
        decrypt_text = decrypt(string, key)
        print("Decrypted message: " + decrypt_text)
```

### Flag
picoCTF{CRYPTOISFUN}
</br>

# The Numbers
## Description
The [numbers](https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png)... what do they mean?

## Writeup
The link refers to a picture (png-file) which contains a string of numbers, representing the position of a letter in the alphabet. This is obvious as the string also contains the curly braces for the flag format 'picoCTF{}'.
With a simple python file the numbers can be converted into the appropiate letters:
```
#!/usr/bin/env python3
orig_message = [16, 9, 3, 15, 3, 20, 6, '{', 20, 8, 5, 14, 21, 13, 2, 5, 18, 19, 13, 1, 19, 15, 14, '}']
flag = []
for i in orig_message:
	if str(i).isalnum():
		char = chr((65 - 1) + int(i)) # 65 is for 'A' in ASCII, -1 as numbering in regular Alphabet does not start at 0
		flag.append(char)
	else:
		flag.append(i)
print("".join(flag))
```

### Flag
PICOCTF{THENUMBERSMASON}
<br/>

# 13
## Description
Cryptography can be easy, do you know what ROT13 is?
**cvpbPGS{abg_gbb_onq_bs_n_ceboyrz}**

## Writeup
ROT13 refers to the Ceasar Cipher, where you shift each letter in a sentence or word by 13 places up the alphabet - e.g. 'A' becomes 'N' and so on.
Either search for a Ceasar/ROT13 decrypter online, like on [ASCII to Hex](https://www.asciitohex.com/) or Python can be our friend here as well:

```
#!/usr/bin/env python3
ROT = 13

def decrypt(message):
    decrypt_text = []
    for i in range(len(message)):
        if message[i].isalpha():
            if message[i].isupper():
                c = ord(message[i]) - ord('A')
                c = ((c - ROT) % 26) + ord('A')
            else:
                c = ord(message[i]) - ord('a')
                c = ((c - ROT) % 26) + ord('a')
            decrypt_text.append(chr(c))
        else:
            decrypt_text.append(message[i])
    return("".join(decrypt_text))

def encrypt(message):
    encrypt_text = []
    for i in range(len(message)):
        if message[i].isalpha():
            if message[i].isupper():
                c = ord(message[i]) - ord('A')
                c = ((c + ROT) % 26) + ord('A')
            else:
                c = ord(message[i]) - ord('a')
                c = ((c + ROT) % 26) + ord('a')
            decrypt_text.append(chr(c))
        else:
            decrypt_text.append(message[i])
    return("".join(encrypt_text))

if __name__ == "__main__":
    encrypt = input("Would you like to encrypt a message [Y]/[N]: ")
    if encrypt == 'Y':
        string = input("Enter message to encrypt: ")
        encrypt_text = encrypt(string)
        print("Encrypted message: " + encrypt_text)
    else:
        string = input("Enter message to decrypt: ")
        decrypt_text = decrypt(string)
        print("Decrypted message: " + decrypt_text)
```

### Flag
picoCTF{not_too_bad_of_a_problem}
<br/>

# caesar
## Description
Decrypt this [message](https://jupiter.challenges.picoctf.org/static/49f31c8f17817dc2d367428c9e5ab0bc/ciphertext).

## Writeup
The message contains the encrypted flag **picoCTF{ynkooejcpdanqxeykjrbdofgkq}**. Based on the name of the challenge we can assume its a Caesar cipher, similar to the ROT13 challenge we solved before. But in this case we do not know how many times the letters were shifted, i.e. it does not have to be 13 times like with ROT13.

We still can use the Python script we created for the ROT13 challenge and adapt it to the new challenge, so we loop through shifts from 2 to 25 (max possible shifts, as the alphabet only has 26 letters)

Doing this, we get the following decrypted messages:
```
Decrypted message 0: ynkooejcpdanqxeykjrbdofgkq
Decrypted message 1: xmjnndiboczmpwdxjiqacnefjp
Decrypted message 2: wlimmchanbylovcwihpzbmdeio
Decrypted message 3: vkhllbgzmaxknubvhgoyalcdhn
Decrypted message 4: ujgkkafylzwjmtaugfnxzkbcgm
Decrypted message 5: tifjjzexkyvilsztfemwyjabfl
Decrypted message 6: sheiiydwjxuhkrysedlvxizaek
Decrypted message 7: rgdhhxcviwtgjqxrdckuwhyzdj
Decrypted message 8: qfcggwbuhvsfipwqcbjtvgxyci
Decrypted message 9: pebffvatgurehovpbaisufwxbh
Decrypted message 10: odaeeuzsftqdgnuoazhrtevwag
Decrypted message 11: nczddtyrespcfmtnzygqsduvzf
Decrypted message 12: mbyccsxqdrobelsmyxfprctuye
Decrypted message 13: laxbbrwpcqnadkrlxweoqbstxd
Decrypted message 14: kzwaaqvobpmzcjqkwvdnparswc
Decrypted message 15: jyvzzpunaolybipjvucmozqrvb
Decrypted message 16: ixuyyotmznkxahoiutblnypqua
Decrypted message 17: hwtxxnslymjwzgnhtsakmxoptz
Decrypted message 18: gvswwmrkxlivyfmgsrzjlwnosy
Decrypted message 19: furvvlqjwkhuxelfrqyikvmnrx
Decrypted message 20: etquukpivjgtwdkeqpxhjulmqw
Decrypted message 21: dspttjohuifsvcjdpowgitklpv
Decrypted message 22: crossingtherubiconvfhsjkou
Decrypted message 23: bqnrrhmfsgdqtahbnmuegrijnt
Decrypted message 24: apmqqglerfcpszgamltdfqhims
```

One of those does look like its not only jibberish - message 22. Flag found!

### Flag
picoCTF{crossingtherubiconvfhsjkou}