+++
date = "2021-03-03"
title = "118. Pascal triangle"
tags = ["leetcode","bit"]
+++

Input: 5 
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]

- code, better
```py
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        def generate_next(lines):
            lastline = lines[-1]
            next = [1]
            for i in range(len(lastline)-1):
                next.append(lastline[i]+lastline[i+1])
            next.append(1)
            lines.append(next)
            return lines

        if numRows == 1:
            return [[1]] 
        return generate_next(self.generate(numRows-1))

```
- c
```py
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        if numRows == 0:
            return []
        n1 = [1]
        n2 = [1,1]
        if numRows == 1:
            return [n1]
        if numRows == 2:
            return [n1,n2]
        
        last = self.generate(numRows-1)
        lastline = last[-1]
        newline = [1]
        for i in range(len(lastline)-1):
            newline.append(lastline[i]+lastline[i+1])
        newline.append(1)    
        last.append(newline)
        return last
```
