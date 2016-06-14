---
layout: post
title: "Python bruteforce password generator"
date: 2014-04-09 21:38:35 +0200
comments: true
categories: 
---
Generating char combinations is extremely easy with Python's itertools.

``` python
import string
import itertools

def dict_gen_up_to_len(n):
    chars = string.ascii_letters + string.digits + '!@#$%^&*()'
    return itertools.chain(''.join(j) for i in range(n) for j in itertools.product(chars, repeat=i+1))

def dict_gen_exact_len(n):
    chars = string.ascii_letters + string.digits + '!@#$%^&*()'
    return itertools.chain(''.join(j) for j in itertools.product(chars, repeat=n))

n = 8

for word in dict_gen_exact_len(n):
    print (word)

# aaaaaaaa
# aaaaaaab
# aaaaaaac
# ...
# ))))))))

for word in dict_gen_up_to_len(n):
    print (word)

# a
# b
# c
# ...
# aa
# ab
```

