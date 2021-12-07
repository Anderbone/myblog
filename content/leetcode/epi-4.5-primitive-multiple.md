+++ 
date = "2020-05-15"
title = "Primitive Multiple"
tags = ["epi","bit"]
+++

## EPI python 4.5
> Use bit manipulation to multiple.

Iterate through the bits of x, adding the $2^ky$ to the result if the kth bit of x is 1.

### java

```java
    public static long multiply(long x, long y) {

        long res = 0;
        while (x != 0) {
            if ((x&1) != 0) {
                res = add(res, y);
            }
            x >>= 1;
            y <<= 1;
        }
        return res;
    }

    private static long add(long x, long y) {
        long carry;

        while (y != 0) {
            carry = x & y;
            x = x ^ y;
            y = carry << 1;
        }
        return x;

//  A single line add function
//  return b == 0 ? a : add(a ^ b, (a & b) << 1);
    }

```

### python
```python
    public static long multiply(long x, long y) {

        long res = 0;
        while (x != 0) {
            if ((x&1) != 0) {
                res = add(res, y);
            }
            x >>= 1;
            y <<= 1;
        }
        return res;
    }

    private static long add(long x, long y) {
        long carry;

        while (y != 0) {
            carry = x & y;
            x = x ^ y;
            y = carry << 1;
        }
        return x;
//        return b == 0 ? a : add(a ^ b, (a & b) << 1);

    }
```
