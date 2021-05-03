---
title: "vault-door-1"
subtitle: Reverse Engineering
date: 2021-05-03T19:53:11+02:00
tags: ['picoCTF', 'RevEng', 'itsec']
draft: true
---

This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: [VaultDoor1.java](https://jupiter.challenges.picoctf.org/static/ff2585f7afd21b81f69d2fbe37c081ae/VaultDoor1.java)

<!--more-->

## Writeup
There is a new check in the Java File with the String function `charAt`, where it compares the input with the specified chars necessary at each position. We can manually get the corresponding char for each position ('easier') or with a Python script:

``` python
#!/usr/bin/env python3
import operator
import re
from pathlib import Path

path = Path.cwd()
file = open(path/'VaultDoor1.java')
input = file.read()

regex = re.compile(r'''\(\d{1,2}\)''')
regex2 = re.compile(r'\'[a-zA-Z0-9_]\'')
key = re.findall(regex, input)
value = re.findall(regex2, input)

for i in range(len(key)):
    length = len(key[i]) - 1
    key[i] = int(key[i][1:length])
for k in range(len(value)):
    length = len(value[k]) - 1
    value[k] = value[k][1:length]

new_dict = dict(zip(key, value))
sorted_dict = dict(sorted(new_dict.items(), key=operator.itemgetter(0)))

text = []
print("picoCTF{", end="")
for key,value in sorted_dict.items():
    print(value, end="")
print("}")
print("")

```

### Flag
picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_75092e}