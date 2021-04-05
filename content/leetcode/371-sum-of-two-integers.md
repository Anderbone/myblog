+++
date = "2021-04-02"
title = "371. Sum of two integers"
tags = ["leetcode","primitive"]
+++


Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

- code
```py
class Solution:
    def getSum(self, a: int, b: int) -> int:
        if a == 0:
            return b
        elif b == 0:
            return a

        mask = 0xffffffff

        # print(-1&mask)
        while b != 0:
            a, b = (a ^ b) & mask, ((a & b) << 1) & mask

        # a is negative if the first bit is 1
        if (a >> 31) & 1:
            return ~(a ^ mask)
        else:
            return a  

```
- c0
```py
class Solution:
    def getSum(self, a: int, b: int) -> int:
        
        mask = 0xffffffff
        
        while b & mask:
            _carry = a & b
            a = a ^ b
            b = _carry << 1
        
        # for overflow condition like
        # -1
        #  1
        return (a & mask) if b > mask else a
```
- c java
```java
int AddWithoutArithmetic(int num1, int num2)
{
        if(num2 == 0)
                return num1;
 
        int sum = num1 ^ num2;
        int carry = (num1 & num2) << 1;
 
        return AddWithoutArithmetic(sum, carry);
}
```

for py [https://leetcode.com/problems/sum-of-two-integers/discuss/84350/Most-Straightforward-Python-Solution!](https://leetcode.com/problems/sum-of-two-integers/discuss/84350/Most-Straightforward-Python-Solution!)
Idea:
Adding two integers a and b (no matter positive or negative) can always be boiled down into 3 steps:


	convert a and b into two's complements.
	add both two's complements. The result is a new two's complement
	convert the result back to integer
Two things to note:


	In Python, every integer is associated with its two's complement and its sign. However, doing bit operation "& mask" loses the track of sign. For example, -1 & 0xffffffffbecomes a huge positive number 4294967295. Therefore, after the while loop, a is the two's complement of the final result as a 32-bit unsigned integer.
	The magic is that if there is a negative integer n, and its unsigned 32-bit two's complement is m, then m = ~(n ^ 0xffffffff) and n = ~(m ^ 0xffffffff). So using this magic, you can do the conversion in step 3.
