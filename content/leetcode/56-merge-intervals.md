+++
date = "2021-03-22"
title = "56. Merge internals"
tags = ["leetcode","sorting"]
+++

Given a collection of intervals, merge all overlapping intervals.
Example 1:
Input: [[1,3],[2,6],[8,10],[15,18]] Output: [[1,6],[8,10],[15,18]] Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

- code
```py
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        res = [intervals[0]]
        for each in range(1, len(intervals)):
            cur_start = intervals[each][0]
            cur_end = intervals[each][1]
            last_end = res[-1][1]
            if cur_start <= last_end:
                res[-1][1] = max(cur_end, last_end)
            else:
                res.append(intervals[each])
        return res
```
