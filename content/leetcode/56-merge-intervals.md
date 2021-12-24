+++
date = "2021-03-22"
title = "56. Merge internals"
tags = ["leetcode","sorting"]
+++
[Merge Intervals - LeetCode](https://leetcode.com/problems/merge-intervals/)

Given a collection of intervals, merge all overlapping intervals.
Example 1:
Input: [[1,3],[2,6],[8,10],[15,18]] Output: [[1,6],[8,10],[15,18]] Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

---
- code
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a,b)-> a[0]-b[0]);
        LinkedList<int []> merged = new LinkedList();
        merged.offer(intervals[0]);
        for (int i = 1; i < intervals.length; ++i){
            if (intervals[i][0] > merged.peekLast()[1]){
                merged.offer(intervals[i]);
            }else{
                merged.peekLast()[1] = Math.max(merged.peekLast()[1], intervals[i][1]);
            }
        }
        return merged.toArray(new int[merged.size()][]);
    }
}
```
- code
```py
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        res = [intervals[0]]
        for i in range(1, len(intervals)):
            if intervals[i][0] <= res[-1][1]:
                res[-1][1] = max(res[-1][1], intervals[i][1])
            else:
                res.append(intervals[i])
        return res
```
