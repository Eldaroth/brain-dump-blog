---
title: The_Numbers
subtitle: Cryptography
date: 2021-03-12
tags: ['picoCTF', 'cryptography', 'itsec']
draft: false
---

The [numbers](https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png)... what do they mean?

<!--more-->

![the_numbers.png](/img/the_numbers.png)

## Writeup
The link refers to the image above (png-file) on which we can see a string of numbers, each representing the position of a letter in the alphabet. Why do I think this is the case? Because the string also contains the curly braces for the flag format 'picoCTF{}', which indicates before and after the curly braces has to be some more text.
With a simple Python script the numbers can be converted into the appropiate letters in the alphabet:

**numbers.py**
```
#!/usr/bin/env python3
orig_message = [16, 9, 3, 15, 3, 20, 6, '{', 20, 8, 5, 14, 21, 13, 2, 5, 18, 19, 13, 1, 19, 15, 14, '}']
flag = []
for i in orig_message:
	if str(i).isalnum():
		char = chr((65 - 1) + int(i))
                # 65 is for 'A' in ASCII,
                # -1 as numbering in regular Alphabet does not start at 0
		flag.append(char)
	else:
		flag.append(i)
print("".join(flag))
```

### Flag
PICOCTF{THENUMBERSMASON}
