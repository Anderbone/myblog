+++ 
date = "2021-03-08"
title = "49. Group anagrams"
tags = ["leetcode","array"]
+++

Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]

- code  notice after sorted "eat", it becomes ['a','e','t']
```py
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        dic_ana = {}
        for word in strs:
            sword = "".join(sorted(word))
            if sword not in dic_ana:
                dic_ana[sword] = [word]
            else:
                dic_ana[sword].append(word)
        
        return [v for v in dic_ana.values()]

```
