+++
date = "2021-02-13"
title = "108. Convert sorted array to binary search tree"
tags = ["leetcode","tree"]
+++

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.
For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of everynode never differ by more than 1.
Example:
Given the sorted array: [-10,-3,0,5,9], One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
      0
     / \
   -3   9
   /   /
 -10  5

- code
```py
class Solution:

    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        if not nums:
            return None
        
        mid = len(nums)//2
        head = TreeNode(nums[mid])
        head.left = self.sortedArrayToBST(nums[:mid])
        head.right = self.sortedArrayToBST(nums[mid+1:])
        
        return head
```
