+++ 
date = "2020-12-25"
title = "Compute rows in Pascal's triangle"
tags = ["string"]
+++

take a string representing an integer and return the corresponding integer, and vice versa, should handle negative integers.  
Implement an integer to string conversion function, and a string to integer.  
Cannot use library like 'int'.

 string.digits = '0~9', then index, to change str to int
  better, `res * (-1 if ... else 1) `
 - str to int
- code same, just shorter
```python
def string_to_int(s: str) -> int:

    return (-1 if s[0] == '-' else 1) * functools.reduce(
        lambda running_sum, c: running_sum * 10 + string.digits.index(c),
        s[s[0] in '-+':], 0)
```
- code
```python
def string_to_int(s: str) -> int:
    f = lambda x, y: x*10 + string.digits.index(y)
    res = functools.reduce(f,s[s[0] in '-+':], 0) # need to use 0 as initial, since x*10 in the first round
    # res = functools.reduce(f, s[1:], 0) # need to use 0 as initial, since x*10 in the first round
    if s[0] == '-':
        return -res
    return res
```
- int to string
  
  the least significant digit in the decimal representation of r is r mod 10
  423 % 10 = 3   then 423 // 10 = 42
  `chr(ord('0') + 3)` to get str '3'
- c
```python
def int_to_string(x):
    print(x)

    is_negative = False
    if x < 0:
        x, is_negative = -x, True

    s = []
    while True:
        s.append(chr(ord('0') + x % 10))
        x //= 10
        if x == 0:
            break

    # Adds the negative sign back if is_negative
    print(('-' if is_negative else '') + ''.join(reversed(s)))
    return ('-' if is_negative else '') + ''.join(reversed(s))
```
