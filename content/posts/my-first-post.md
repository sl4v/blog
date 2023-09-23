---
title: "My First Post"
date: 2022-11-20T09:03:20-08:00
draft: true
---

![Scenario 1: Across columns](/1.jpg)

## Introduction

This is **bold** text, and this is *emphasized* text.

Visit the [Hugo](https://gohugo.io) website!

{{< highlight python "linenos=table" >}}
import string
from binascii import hexlify

l1_q1 = ['P', 'H', 'P', 'U']
l1_q2 = ['V', 'K', 'P', 'K']
l1_q3 = ['V', 'G', 'V', 'Z']
l1_q4 = ['V', 'S', 'P', 'N']
l1_q5 = ['V', 'B', 'P', 'B']
l1_q6 = ['V', 'D', 'V', 'D']

l2_q1 = ['O', 'Y', 'Y', 'Y']
l2_q2 = ['O', 'W', 'O', 'K']
l2_q3 = ['Y', 'N', 'Y', 'S']
l2_q4 = ['O', 'D', 'O', 'D']
l2_q5 = ['Y', 'F', 'O', 'F']
l2_q6 = ['H', 'G', 'U', 'Z']

l3_q1 = ['U', 'V', 'U', 'I']
l3_q2 = ['H', 'B', 'U', 'B']
l3_q3 = ['H', 'F', 'H', 'F']
l3_q4 = ['K', 'Z', 'W', 'G']
l3_q5 = ['W', 'B', 'W', 'B']
l3_q6 = ['W', 'D', 'K', 'D']

line_1 = [
    l1_q1,
    l1_q2,
    l1_q3,
    l1_q4,
    l1_q5,
    l1_q6,
]

line_2 = [
    l2_q1,
    l2_q2,
    l2_q3,
    l2_q4,
    l2_q5,
    l2_q6,
]

line_3 = [
    l3_q1,
    l3_q2,
    l3_q3,
    l3_q4,
    l3_q5,
    l3_q6,
]

keys = [
    'PLHSTR',
    'FF06B5',
    'MRPHYM',
    'BLCKHND',
    'ARMSMG',
    'ANTVRK',
    '\xff\x06\xb5\xff\x06\xb5',
    '\x00\x00\x00\x00\x00\x00',
    'FFVQBZ',
]

def char_to_num_ascii(c):
    return ord(c)

def char_to_num_alphabet(c):
    return ord(c) - ord('A')

def char_to_num_map_1(c):
    map_1 = {
        'P': 1,
        'H': 2,
        'U': 3,
        'V': 4,
        'K': 5,
        'G': 6,
        'Z': 7,
        'S': 8,
        'N': 9,
        'B': 10,
        'D': 11,
        'O': 12,
        'Y': 13,
        'W': 14,
        'F': 15,
        'I': 16
    }
    n = map_1.get(c)
    if n:
        return n-1
    else:
        return 0

def char_to_num_map_1_1(c):
    return char_to_num_map_1(c) + 1

def char_to_num_map_2(c):
    map_2 = {
        'P': 1,
        'H': 2,
        'U': 3,
        'V': 4,
        'K': 5,
        'G': 6,
        'Z': 7,
        'S': 8,
        'N': 9,
        'B': 10,
        'D': 11,
        'O': 12,
        'Y': 13,
        'W': 14,
        'F': 15,
        'I': 16
    }
    n = map_2.get(c)
    if n:
        return n-1
    else:
        return 0

def char_to_num_map_2_1(c):
    return char_to_num_map_2(c) + 1

char_conv_l = [
    char_to_num_ascii,
    char_to_num_alphabet,
    char_to_num_map_1,
    char_to_num_map_1_1,
    char_to_num_map_2,
    char_to_num_map_2_1
]

def num_to_char_ascii(n):
    return chr(n)

def num_to_char_alphabet(n):
    return chr(n + ord('A'))

def num_to_char_map_1(n):
    map_1 = {
        1: 'P',
        2: 'H',
        3: 'U',
        4: 'V',
        5: 'K',
        6: 'G',
        7: 'Z',
        8: 'S',
        9: 'N',
        10: 'B',
        11: 'D',
        12: 'O',
        13: 'Y',
        14: 'W',
        15: 'F',
        16: 'I'
    }

    c = map_1.get(n)
    if c:
        return c
    else:
        return '?'

def num_to_char_map_1_1(n):
    return num_to_char_map_1(n+1)

def num_to_char_map_2(n):
    map_2 = {
        1: 'B',
        2: 'D',
        3: 'F',
        4: 'G',
        5: 'H',
        6: 'I',
        7: 'K',
        8: 'N',
        9: 'O',
        10: 'P',
        11: 'S',
        12: 'U',
        13: 'V',
        14: 'W',
        15: 'Y',
        16: 'Z'
    }

    c = map_2.get(n)
    if c:
        return c
    else:
        return '?'

def num_to_char_map_2_1(n):
    return num_to_char_map_2(n+1)

num_to_char_l = [
    num_to_char_ascii,
    num_to_char_alphabet,
    num_to_char_map_1,
    num_to_char_map_1_1,
    num_to_char_map_2,
    num_to_char_map_2_1,
]

def op_add(n1, n2):
    return n1 + n2

def op_xor(n1, n2):
    return n1 ^ n2

def op_min(n1, n2):
    return n1 - n2

op_l = [
    op_add,
    op_xor,
    op_min
]

def solve_generic(char_to_num, op_1, op_2, num_to_char, line, key, m):
    res = ''
    for i in range(len(line)):
        qube = line[i]
        sum = 0
        for c in qube:
            sum = op_1(sum, char_to_num(c))
        sum = op_2(sum, char_to_num(key[i]))
        sum = sum % m
        res = res + num_to_char(sum)
    return res

def solve_mod_2(line, key, m):
    res = ''
    for i in range(len(line)):
        qube = line[i]
        sum = 0
        for c in qube:
            sum += ord(c) - ord('A')
        sum += ord(key[i]) - ord('A')
        sum = sum % m
        res = res + chr(sum + ord('A'))
    return res

def solve_mod_xor(line, key, m):
    res = ''
    for i in range(len(line)):
        qube = line[i]
        sum = 0
        for c in qube:
            sum += ord(c)
        sum ^= ord(key[i])
        sum = sum % m
        res = res + chr(sum)
    return res

def solve_xor(line, key, m):
    res = ''
    for i in range(len(line)):
        qube = line[i]
        sum = 0
        for c in qube:
            sum ^= ord(c)
        sum ^= ord(key[i])
        sum = sum % m
        res = res + chr(sum)
    return res





def analyze_hex():
    flat_l = sum(line_1, []) + sum(line_2, []) + sum(line_3, [])
    print(flat_l)
    print(set(flat_l), len(set(flat_l)))




# for key in keys:
#     for m in [26, 16]:
#         for line in [line_1, line_2, line_3]:
#             # res = solve_mod_xor(line, key, m)
#             # print(repr(res))
#             # res = solve_mod(line, key, m)
#             # print(repr(res))
#             # res = solve_xor(line, key, m)
#             # print(repr(res))
#             res = solve_mod_2(line, key, m)
#             print(repr(res))

analyze_hex()

def check_string(s: str) -> bool:
    # Check for all printable characters
    if not all(char.isprintable() for char in s):
        return False

    # Check for no more than 2 repeated characters in a row
    for i in range(len(s) - 2):
        if s[i] == s[i+1] == s[i+2]:
            return False

    # Check if '?' exists in the string
    if '?' in s:
        return False

    return True

for key in keys:
    print(key)
    for m in [26, 16]:
        print(f'  {m}')
        for line in [line_1]:
            for char_to_num in char_conv_l:
                for num_to_char in num_to_char_l:
                    for op_1 in op_l:
                        for op_2 in op_l:
                            res = solve_generic(char_to_num, op_1, op_2, num_to_char, line, key, m)
                            if (check_string(res)):
                                print(f'    {res}')
{{< / highlight >}}


```python
def check_string(s: str) -> bool:
    # Check for all printable characters
    if not all(char.isprintable() for char in s):
        return False

    # Check for no more than 2 repeated characters in a row
    for i in range(len(s) - 2):
        if s[i] == s[i+1] == s[i+2]:
            return False

    # Check if '?' exists in the string
    if '?' in s:
        return False
```