Reverse Engineering

# vault-door-training
## Description
Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: [VaultDoorTraining.java](https://jupiter.challenges.picoctf.org/static/a4a1ca9c54d8fac9404f9cbc50d9751a/VaultDoorTraining.java)

## Writeup
Looking at the Java File, its quite simple to find out what it does as the "password", i.e. the flag, is written in the code in plaintext.

```
import java.util.*;

class VaultDoorTraining {
    public static void main(String args[]) {
        VaultDoorTraining vaultDoor = new VaultDoorTraining();
        Scanner scanner = new Scanner(System.in); 
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
	}
   }

    // The password is below. Is it safe to put the password in the source code?
    // What if somebody stole our source code? Then they would know what our
    // password is. Hmm... I will think of some ways to improve the security
    // on the other doors.
    //
    // -Minion #9567
    public boolean checkPassword(String password) {
        return password.equals("w4rm1ng_Up_w1tH_jAv4_be8d9806f18");
    }
}
```

### Flag
picoCTF{w4rm1ng_Up_w1tH_jAv4_be8d9806f18}
<br/>

# vault-door-1
## Description
This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: [VaultDoor1.java](https://jupiter.challenges.picoctf.org/static/ff2585f7afd21b81f69d2fbe37c081ae/VaultDoor1.java)

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
<br/>
