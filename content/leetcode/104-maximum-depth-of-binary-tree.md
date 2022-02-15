+++ 
date = "2022-02-14"
title = "104. Maximum Depth of Binary Tree"
tags = ["binarytree"]
+++
[Maximum Depth of Binary Tree - LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Given the root of a binary tree, return __its maximum depth__.
A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
 
Example 1:
![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)Input: root = [3,9,20,null,null,15,7] Output: 3 
Example 2:
Input: root = [1,null,2] Output: 2 
 
Constraints:

	The number of nodes in the tree is in the range [0, 104].
	-100 <= Node.val <= 100
---
- code
```py
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))

```
- c iteration
```py
class Solution:
    def maxDepth(self, root):
        if not root: return 0 
        level = [root]; depth = 0
        while level:
            depth += 1
            level = [i for n in level for i in (n.left, n.right) if i]
        return depth
   ```
- code stack iteration
```py
class Solution:
    def maxDepth(self, root):
        stack = []
        if root:
            stack.append((1, root))
        
        depth = 0
        while stack:
            current_depth, root = stack.pop()
            if root:
                depth = max(depth, current_depth)
                stack.append((current_depth + 1, root.left))
                stack.append((current_depth + 1, root.right))
        
        return depth
```
