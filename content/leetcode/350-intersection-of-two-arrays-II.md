+++
date = "2021-01-06"
title = "350. Intersection of two arrays II"
tags = ["array"]
+++


Given two arrays, write a function to compute their intersection.  
Example 1:
Input: nums1 = [1,2,2,1], nums2 = [2,2]Output: [2,2]  
Example 2:
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]Output: [4,9]

- c0
```python
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        d1 = dict(collections.Counter(nums1))
        d2 = dict(collections.Counter(nums2))
        ans = []
        for i in d1:
            if i in d2:
                count = min(d1[i],d2[i])
                ans.extend(count*[i])
        return ans
```
- code, hash table (similar to c0 without second dic), and sorted with pointer
```python
# Hash table
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # Traverse the shorter array and store the elements in the hash table
        # Ensure that the previous array is short
        if len(nums1) > len(nums2):
            self.intersect(nums2, nums1)
        
        hash_map = {}

        for num in nums1:
            if num not in hash_map:
                hash_map[num] = 0
            hash_map[num] += 1
        
        ans = []

        for num in nums2:
            # Check if it exists in the hash table
            count = hash_map.get(num, 0)
            # If the element exists in the hash table, it is added to the result list
            # Then reduce the number of occurrences of the element corresponding to the hash table by one
            if count > 0:
                ans.append(num)
                hash_map[num]-=1
        
        return ans

# Double pointer
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        nums1.sort()
        nums2.sort()

        p = q = 0

        ans = []
        # Arbitrary pointer reaches the end of the array, end traversal
        while p < len(nums1) and q < len(nums2):
            # Here, first determine the size of the element corresponding to the pointer
            # When not equal, the pointer corresponds to a small movement of the element
            # When equal, put the elements into the result list and move the pointer at the same time
            if nums1[p] > nums2[q]:
                q+=1
            elif nums1[p] < nums2[q]:
                p += 1
            else:
                ans.append(nums1[p])
                p += 1
                q += 1
        
        return ans

```
