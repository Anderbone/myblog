+++
date = "2021-03-27"
title = "300. Longest increasing subsequence"
tags = ["dp"]
+++

Given an unsorted array of integers, find the length of longest increasing subsequence. A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

Example:
Input: [10,9,2,5,3,7,101,18] Output: 4 Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 

- code, time limit exceeded
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums:
            return 0
        first_list = [nums[0]]
        longest = 1
        all_list = [first_list]
        for v in nums:
            for cur_list in all_list:
                # print(cur_list)
                if v < cur_list[0]:
                    all_list.append([v])
                elif v > cur_list[-1]:
                    cur_list.append(v)
                elif cur_list[0] < v < cur_list[-1] and v not in cur_list:
                    for i,cur in enumerate(cur_list):
                        if v < cur:
                            cur_list[i] = v
                            break
        longest = max(len(each) for each in all_list)
        return longest



```
subsequence is always related to find and exchange the one in order.
- c, binary search
```py
   # (方法二)
    # O(nlogn)
    # L[i]中i表示以L[i]结尾的最长递增子序列的长度, 维护的L[i]是最小的
    
class Solution: 
    def lengthOfLIS(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        L = [nums[0]]
        
        for i in range(1, len(nums)):
            if nums[i] > L[-1]:
                L.append(nums[i])
            else:
                # 二分查找替换掉大于等于nums[i]的最小的数字
                left = 0
                right = len(L) - 1
                while left <= right:
                    # mid = (left + right) // 2
                    mid = left + (right-left)//2
                    if nums[i] < L[mid]:
                        right = mid -1 
                    elif nums[i] > L[mid]:
                        left = mid + 1
                    else:
                        left = mid
                        break
                # 替换
                L[left] = nums[i]
        return len(L)
```
- c1 
```py
class Solution: 
    def lengthOfLIS(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
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
