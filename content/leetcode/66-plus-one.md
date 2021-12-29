+++
date = "2021-01-06"
title = "66. Plus One"
tags = ["array"]
+++

Given a non-empty array of digits representing a non-negative integer, plus one to the integer.
The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.
You may assume the integer does not contain any leading zero, except the number 0 itself.  
Example 1:
Input: [1,2,3] Output: [1,2,4] Explanation: The array represents the integer 123.
```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        for i in reversed(range(len(digits))):
            if digits[i] != 9:
                digits[i] += 1
                return digits
            else:
                digits[i] = 0
                if i == 0:
                    digits.insert(0, 1)
        return digits
```
code py
```python
def plus_one(A):

    A[-1] += 1
    for i in reversed(range(1, len(A))):
        if A[i] != 10:
            break
        A[i] = 0
        A[i - 1] += 1
    if A[0] == 10:
        # There is a carry-out, so we need one more digit to store the result.
        # A slick way to do this is to append a 0 at the end of the array,
        # and update the first entry to 1.
        A[0] = 1
        A.append(0)
    return A

```
code java
```java
public static List<Integer> plusOne(List<Integer> A) {
    A.set(A.size()-1, A.get(A.size()-1) + 1);
    for (int i = A.size()-1; i>0 && A.get(i) == 10; i--) {
      A.set(i, 0);
      A.set(i-1, A.get(i-1)+1);
    }
    if (A.get(0) == 10) {
        A.set(0, 1);
        A.add(0);// add at the end.  999->1000
    }
    return A;
  }
```
- c  no, brute-force
```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        s = "".join(str(i) for i in digits)
        num = int(s)
        ans = num+1
        s = str(ans)
        final = []
        for i in list(s):
            final.append(int(i))
        return final
```
