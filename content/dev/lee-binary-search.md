+++
date = "2022-07-10"
title = "leetcode questions: Binary Search"
tags = ["binarysearch","leetcode summary"]
toc = true
+++

### [300 Longest Increasing Subsequence](https://yanjiyu.com/leetcode/300/)

> Given an unsorted array of integers, find the length of longest increasing subsequence. A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].  
Example:  
Input: [10,9,2,5,3,7,101,18] Output: 4 Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```py
class Solution: 
    def lengthOfLIS(self, nums: List[int]) -> int:
        
        L = [nums[0]]
        
        for i in range(1, len(nums)):
            if nums[i] > L[-1]:
                L.append(nums[i])
            else:
                # binary search to find the smallest number which is bigger than nums[i]                  
                left = bisect.bisect_left(L, nums[i])
 
                L[left] = nums[i]
      # actuaclly 2,3,7,18
        return len(L)
```
- code binary search
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        ArrayList<Integer> sub = new ArrayList<>();
        sub.add(nums[0]);
        
        for (int i = 1; i < nums.length; i++) {
            int num = nums[i];
            if (num > sub.get(sub.size() - 1)) {
                sub.add(num);
            } else {
                int j = binarySearch(sub, num);
                sub.set(j, num);
            }
        }
        
        return sub.size();
    }
    
    private int binarySearch(ArrayList<Integer> sub, int num) {
        int left = 0;
        int right = sub.size();
        int mid = (left + right) / 2;
        
        while (left < right) {
            mid = (left + right) / 2;
            if (sub.get(mid) == num) {
                return mid;
            }
            if (sub.get(mid) < num) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        return left;
    }
}
```
