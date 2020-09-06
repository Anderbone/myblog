+++ 
date = "2020-05-15"
title = "Reverse bits"
tags = ["leetcode","primitive","bit"]
+++


### Leetcode 190 
> Similar question. Reverse bits of a given 32 bits unsigned integer.
 
Example 1:
Input: 00000010100101000001111010011100   
Output: 00111001011110000010100101000000   
Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.

With python, we just get all bits in an array and reverse it, then turn it back to a number.
```python
class Solution:
    # @param n, an integer
    # @return an integer
    def reverseBits(self, n):

        s = str(bin(n)).replace('0b','')
        s = '0'*(32-len(s)) + s
        ans = s[::-1]
        return int(ans, 2)
```


 ```python   
 a = format(n,"032b")
return int(a[::-1],2)
```

### 5.3 in EPI java, 4.3 in EPI python. 
> Return the 64-bit word consisting of the bits of the input word in reverse order.

The simple way is to go through all bits, get the last bit and put it in a result number, then move both number to an opposite direction.

```java
public static long reverseBits(long x) {
    long result = 0;
    int count = 0;
    while (x > 0) {
        count++;
        short rightBit = (short) (x & 1);
        result = (result << 1) + rightBit;
        x >>= 1;
    }
    result <<= (64 - count); // add 0 to the end
    return result;
}
```
I still don't know why we need to add 0 to the end, it's not clarified in the original question. The time complexity is O(n), for n-bit integers.

#### Advanced solution using a lookup table

Build an array-based lookup table A, such that A[y] holds the bit-reversal of y. O(n/L) for n-bit integers and L-bit cache keys.

```java
  private static long reverseBits(long x, int n) {
    for (int i = 0, j = n; i < j; ++i, --j) {
      x = SwapBits.swapBits(x, i, j);
    }
    return x;
  }

  static {
    for (int i = 0; i < (1 << 16); ++i) {
      precomputedReverse[i] = reverseBits(i, 15);
    }
  }

  @EpiTest(testDataFile = "reverse_bits.tsv")
  public static long reverseBits(long x) {

    final int MASK_SIZE = 16;
    final int BIT_MASK = 0xFFFF;
    return precomputedReverse[(int)(x & BIT_MASK)] << (3 * MASK_SIZE) |
        precomputedReverse[(int)((x >>> MASK_SIZE) & BIT_MASK)]
            << (2 * MASK_SIZE) |
        precomputedReverse[(int)((x >>> (2 * MASK_SIZE)) & BIT_MASK)]
            << MASK_SIZE |
        precomputedReverse[(int)((x >>> (3 * MASK_SIZE)) & BIT_MASK)];
  }

```
