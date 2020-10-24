+++ 
date = "2020-07-19"
title = "Increament an arbitrary precision integer"
tags = ["leetcode","array"]
+++

### 6.2 in EPI java, 5.2 in EPI python.
> Takes as input an array of digits encoding a decimal number D and updates the array to represetnt the number D+1. For eg. if the input is <1,2,9> then you should update the array to <1,3,0>.

A brute-force approach might be to convert the array to integer, add one and convert back. If integer had a limit of range this method will fail.

The method below is smarter, time complexity is O(n), n is the length of A.
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