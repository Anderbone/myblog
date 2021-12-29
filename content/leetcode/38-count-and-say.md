+++ 
date = "2021-01-14"
title = "38. count and say"
tags = ["string"]
+++
Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
- code
```python
class Solution:
    def countAndSay(self, n: int) -> str:
        def generator(strin):
            res = []
            last_char = strin[0]
            count_last_char = 1
            for i in range(1, len(strin)):
                if strin[i] != last_char:
                    res.append(str(count_last_char))
                    res.append(last_char)
                    count_last_char = 1
                    last_char = strin[i]
                elif strin[i] == last_char:
                    count_last_char += 1
            res.append(str(count_last_char))
            res.append(last_char)
            return "".join(res)

        if n == 1:
            return "1"
        return generator(self.countAndSay(n-1)) 
```
- c
```python
class Solution:
    def countAndSay(self, n: int) -> str:
        if n == 1:
            return '1'
# easy to compare with the *, for s[i+1] at last round
        s = self.countAndSay(n-1)+'*'   
        ans = ''
        count = 1
        for i in range(len(s)-1):
            if s[i] == s[i+1]:
                count += 1
            else:
                ans = ans+ str(count)+s[i]
                count = 1
        return ans
```
