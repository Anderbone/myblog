+++
date = "2021-02-16"
title = "278. First bad version"
tags = ["leetcode","sort"]
+++

Given n = 5, find the first bad version. (version = 4 is the first bad version.)

call isBadVersion(3) -> false  
call isBadVersion(5) -> true  
call isBadVersion(4) -> true  

Then 4 is the first bad version.

- code
```python
class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        begin, end = 1, n
        while begin < end:
            mid = (begin + end) // 2

            if isBadVersion(mid):
                end = mid
            else:
                begin = mid + 1

        return end

```
- c2
```python
class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        lo, hi = 1, n
        while lo <= hi:
            mid = (lo + hi) // 2
            if isBadVersion(mid):
                hi = mid-1
            else:
                lo = mid+1
 # why return lo here, since lo>hi now, lo's left is always right, hi's right is alwasy wrong
        return lo
```
        
