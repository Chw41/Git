---
title: 'Conflict CTF writeup'
disqus: hackmd
---

Conflict CTF writeup
===

## Table of Contents

[TOC]


## Fork the Topic 
```
git clone https://github.com/ntut-xuan/ConflictCTF.git
```
![image](https://hackmd.io/_uploads/r1Hd_4uyA.png)


```
git checkout master
git merge origin/alice
```
![image](https://hackmd.io/_uploads/SJ1w_V_y0.png)

```
git merge origin/bob // Solve the conflict.
```
![image](https://hackmd.io/_uploads/B1EQQZ4xC.png)

# Topic
## script.py
```python=
<<<<<<< HEAD
#flag_format = "flag{FLAG_HERE}"

alice = ['0x62', '0x6f', '0x6f', '0x6c', '0x72', '0x6e', '0x63', '0x6e', '0x69', '0x72', '0x76', '0x6e', '0x5f', '0x75', '0x65', '0x75', '0x73', '0x5f', '0x69', '0x7b', '0x61', '0x66']
bob = []

def make_the_list_into_char_list(list: list[str]) -> list[str]:
    array = []
    for i in range(len(list)):
        array.append(chr(int(list[i], base=16)))
    return array

def reverse_the_list(list: list[str]) -> list[str]:
=======
import random

# flag_format = "flag{FLAG_HERE}"

alice = []
bob = ['0x81', '0x6a', '0x7c', '0x66', '0x6f', '0x7b', '0x71', '0x66', '0x77', '0x7b', '0x6e', '0x62', '0x6b', '0x6d', '0x67', '0x79', '0x64', '0x69', '0x75', '0x68', '0x6d', '0x6c']

def make_the_list_into_char_list(array):
    return list(map(chr, [int(x, base=16) for x in array]))

def reverse_the_list(list):
>>>>>>> origin/bob
    array = []
    for i in range(len(list)):
        array.append(list[len(list)-1-i])
    return array

def decrease(list):
    random.seed("bob")
    for i in range(len(list)):
        list[i] = hex(int(list[i], base=16) - int(random.random() * 10))
    return list

def make_flag(alice_key, bob_key):
    for i in range(len(alice_key)):
        print(alice_key[i], end="")
        print(bob_key[i], end="")
    print()

make_flag(
    make_the_list_into_char_list(reverse_the_list(alice)), 
    make_the_list_into_char_list(reverse_the_list(decrease(bob)))
<<<<<<< HEAD
)
=======
)
>>>>>>> origin/bob

```
```
python3 script.py
```
![image](https://hackmd.io/_uploads/SJO9OEdyA.png)
> Error

# Solution
## Slove the conflict
vscode debug script.py
```python=

import random

# flag_format = "flag{FLAG_HERE}"

alice = ['0x62', '0x6f', '0x6f', '0x6c', '0x72', '0x6e', '0x63', '0x6e', '0x69', '0x72', '0x76', '0x6e', '0x5f', '0x75', '0x65', '0x75', '0x73', '0x5f', '0x69', '0x7b', '0x61', '0x66']
bob = ['0x81', '0x6a', '0x7c', '0x66', '0x6f', '0x7b', '0x71', '0x66', '0x77', '0x7b', '0x6e', '0x62', '0x6b', '0x6d', '0x67', '0x79', '0x64', '0x69', '0x75', '0x68', '0x6d', '0x6c']

def make_the_list_into_char_list(array):
    return list(map(chr, [int(x, base=16) for x in array]))

def reverse_the_list(list):

    array = []
    for i in range(len(list)):
        array.append(list[len(list)-1-i])
    return array

def decrease(list):
    random.seed("bob")
    for i in range(len(list)):
        list[i] = hex(int(list[i], base=16) - int(random.random() * 10))
    return list

def make_flag(alice_key, bob_key):
    for i in range(len(alice_key)):
        print(alice_key[i], end="")
        print(bob_key[i], end="")
    print()

make_flag(
    make_the_list_into_char_list(reverse_the_list(alice)), 
    make_the_list_into_char_list(reverse_the_list(decrease(bob)))
)

```

```
python3 script.py
```
![image](https://hackmd.io/_uploads/r1mfK4OJR.png)
# Get Flag
> flag{git_is_useful_version_control_owobb}
