
+++ 
date = "2021-04-09"
title = "299. Bulls and cows"
tags = ["array"]
+++


Input: secret = "1807", guess = "7810"

Output: "1A3B"
                        
Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.

terate over the secret string, store all the bulls in an array and keep track of the count for each character that isn't a bull in another array
tput: "1A3B"
 x fasd
Iterate over guess string, if the character isn't a bull, then remove the count of that character and increment cows

- code
```py
class Solution:
    def getHint(self, secret: str, guess: str) -> str:
        s, g = collections.Counter(secret), collections.Counter(guess)
        a = sum(i == j for i, j in zip(secret, guess))
        return '%sA%sB' % (a, sum((s & g).values()) - a)
        

```
eg
Your Input
"1807" "7810" 
Output (60 ms)
"1A3B" 

        print(s&g)
        print((s&g).values())
        print(sum((s&g).values()))

Counter({'1': 1, '8': 1, '0': 1, '7': 1}) dict_values([1, 1, 1, 1]) 4
- code
```py

class Solution:
    def getHint(self, secret: str, guess: str) -> str:
        bulls = cows = 0
        d = collections.defaultdict(int)
        for i, c in enumerate(secret):
            if c == guess[i]:
                bulls += 1
            else:
                d[c] += 1
        for i, c in enumerate(guess):
            if c != secret[i] and c in d and d[c] > 0:
                cows += 1
                d[c] -= 1
        return str(bulls) + "A" + str(cows) + "B"

```
- code, worst
```py
class Solution:
    def getHint(self, secret: str, guess: str) -> str:
        sl = list(secret)
        gl = list(guess)
        i = b = c = 0
        while i < len(sl):
            if sl[i] == gl[i]:
                b += 1
                del sl[i]
                del gl[i]
                i -= 1
            i += 1

        for v in gl:
            if v in sl:
                c += 1
                sl.remove(v)
        
        return str(b) + "A" + str(c) + "B"

```
