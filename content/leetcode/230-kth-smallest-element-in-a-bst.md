+++
date = "2021-03-13"
title = "230. Kth smallest element in a BST"
tags = ["leetcode","tree","bst"]
+++

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.
Note: 
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.
Example 1:
Input: root = [3,1,4,null,2], k = 1  
 3  
  / \  
 1   4  
  \  
   2  
Output: 1

- code  Iterative
```py
class Solution:
    def kthSmallest(self, root, k):
        stack = []
        while root or stack:
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            k -= 1
            if k == 0:
                return root.val
            root = root.right
            

```
- code recursive
```py
class Solution:
    def kthSmallest(self, root, k):
        self.k = k
        self.res = None
        self.helper(root)
        return self.res

    def helper(self, node):
        if node:
            self.helper(node.left)
            self.k -= 1
            if self.k == 0:
                self.res = node.val
                return
            self.helper(node.right)

```
