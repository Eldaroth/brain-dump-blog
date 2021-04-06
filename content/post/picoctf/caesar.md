---
title: "Caesar"
subtitle: Cryptography
date: 2021-03-28T13:10:40+02:00
tags: ['picoCTF', 'cryptography', 'itsec']
draft: false
---

Decrypt this **message**.

<!--more-->

## Writeup
The message contains the encrypted flag **picoCTF{ynkooejcpdanqxeykjrbdofgkq}**. Based on the name of the challenge we can assume it's a Caesar cipher, similar to the [ROT13 challenge](/posts/picoctf/13) we solved before. But in this case we do not know how many times the letters were shifted, i.e. it does not have to be 13 times like with ROT13.

We still can use the Python script we created for the ROT13 challenge and adapt it to the new challenge, so we loop through shifts from 2 to 25 letters (max possible shifts, as the alphabet only has 26 letters).

To adapt the code for this particular problem, we need to get rid of the constant variable 13 (number of shifts). Instead we add an additional parameter for the decrypt and encrypt function with which we can enter how many letter shifts the program should make. When we invoke the function call we use a for-loop to loop through the 25 possibilites and use the position variable in the for loop as parameter for the letter shift.

```
#!/usr/bin/env python3

def decrypt(message, rot):
    decrypt_text = []
    for i in range(len(message)):
        if message[i].isalpha():
            if message[i].isupper():
                c = ord(message[i]) - ord('A')
                c = ((c - rot) % 26) + ord('A')
            else:
                c = ord(message[i]) - ord('a')
                c = ((c - rot) % 26) + ord('a')
            decrypt_text.append(chr(c))
        else:
            decrypt_text.append(message[i])
    return("".join(decrypt_text))

def encrypt(message, rot):
    encrypt_text = []
    for i in range(len(message)):
        if message[i].isalpha():
            if message[i].isupper():
                c = ord(message[i]) - ord('A')
                c = ((c + rot) % 26) + ord('A')
            else:
                c = ord(message[i]) - ord('a')
                c = ((c + rot) % 26) + ord('a')
            decrypt_text.append(chr(c))
        else:
            decrypt_text.append(message[i])
    return("".join(encrypt_text))

if __name__ == "__main__":
    encrypt = input("Would you like to encrypt a message [Y]/[N]: ")
    if encrypt == 'Y':
        string = input("Enter message to encrypt: ")
        for i in range(25):
            encrypt_text = encrypt(string, i)
            print("Encrypted message {}: ".format(i) + encrypt_text)
    else:
        string = input("Enter message to decrypt: ")
        for i in range(25):
            decrypt_text = decrypt(string, i)
            print("Decrypted message {}: ".format(i) + decrypt_text)
```

By doing this, we get the following decrypted messages:
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