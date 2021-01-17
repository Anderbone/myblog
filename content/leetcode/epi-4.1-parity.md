+++ 
date = "2020-05-06"
title = "Computing the parity of a word"
tags = ["epi","primitive","bit"]
+++

### 5.1 in EPI java, 4.1 in EPI python.
> The parity of a binary word is 1 if the number of 1s is odd; otherwise it's 0.
How to check the parity of a very large number of 64-bit words?

A straight forward(brute-force) solution is to go through the bitwised number, get the last bit every time and check weather it's 1. The time complexity is O(n) where n is the word size.
```java
    public static short parity(long x) {
        short flag = 0;
        while (x > 0) {
            short last = (short) (x & 1);
            flag = (short) (flag ^ last);
            x = x >>> 1;
        }
        return flag;
    }
```

A better way takes advantage of the fact that x&(x-1) replaces the lowest bit that is 1 with 0. E.g. $x = (00101100)_2$, $x\\&(x-1)=(00101000)_2$, the last 1 is replaced with 0.

```java
  public static short parity(long x) {

    short flag = 0;
    while (x != 0) {
        flag ^= 1;
        x = x&(x-1);
    }
    return flag;
  }
```
The time complexity is O(k) where k is the number of bits set to 1.


Python version:
```python
def parity(x):

    result = 0
    while x:
        result ^= x & 1
        x >>= 1
    return result
```
```python
def parity(x):
    res = 0
    while x:
        res ^= 1
        x &= x-1
    return res
```