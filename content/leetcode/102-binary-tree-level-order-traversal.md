+++
date = "2021-02-06"
title = "102. Binary tree level order traversal"
tags = ["leetcode","tree"]
+++


Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
For example:
Given binary tree [3,9,20,null,null,15,7],

3  
/ \  
9  20  
/  \  
15   7

return its level order traversal as:

[ [3], [9,20], [15,7] ]

- code
```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res = []
        level = [root]
        while root and level:
            res.append([node.val for node in level])
            level = [i for node in level for i in (node.left, node.right) if i]
        return res

```
- c0
```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        
        def traversal(root, level, res):
            if not root:
                return
            if len(res) <= level:
                res.append([])
            res[level].append(root.val)
            traversal(root.left, level+1, res)
            traversal(root.right, level+1, res)
            
        res = [[]]
        traversal(root,0,res)
        return res
```

