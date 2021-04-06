+++
date = "2021-04-06"
title = "621. Task scheduler"
tags = ["leetcode","array"]
+++

Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks. Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.
However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.
You need to return the least number of intervals the CPU will take to finish all the given tasks.
 
Example:
Input: tasks = ["A","A","A","B","B","B"], n = 2 Output: 8 Explanation: A -> B -> idle -> A -> B -> idle -> A -> B

- code
```py
class Solution(object):
    def leastInterval(self, tasks, n):
        cnt = collections.Counter(tasks)
# 3, 3 here
# at least need full, not count the items in last round. any type which number<tmax coud be added into here.
        tmax = max(cnt.values())
        full = (tmax-1)*(n+1)
# then count the last round, if == tmax, add the last item to this final round
        for i in cnt.values():
            if i == tmax:
                full += 1
# possibly then tasks is longer than full when n is very small
        return max(full, len(tasks))



```


