+++
date = "2021-03-12"
title = "103. Binary tree zigzag level order traversal"
tags = ["leetcode","tree"]
+++

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).
For example:
Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7

return its zigzag level order traversal as:

[ [3], [20,9], [15,7] ]

- code
```py
def zigzagLevelOrder(self, root):
    queue = collections.deque([root])
    res = []
    while queue:
        r = []
        for _ in range(len(queue)):
            q = queue.popleft()
            if q:
                r.append(q.val)
                queue.append(q.left)
                queue.append(q.right)
        r = r[::-1] if len(res) % 2 else r
        if r:
            res.append(r)
    return res
```
- code
```py
class Solution:
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        direction = 1
        res = []
        cur_level = [root]
        while cur_level:
            cur_level_value = [node.val for node in cur_level]
            cur_level = [i for node in cur_level for i in [node.left, node.right] if i]
            if direction == 1:
                res.append(cur_level_value)
                direction = 0
            elif direction == 0:
                res.append(reversed(cur_level_value))
                direction = 1
        return res

```
- c
```py
class Solution:
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        
        def traversal(root, level, res):
            if not root:
                return
            if len(res) <= level:
                res.append([])
            
            if level%2 == 0:
                res[level].append(root.val)
                # flag = 1
            elif level %2 == 1:
                res[level].insert(0, root.val)
                
            traversal(root.left, level+1, res)
            traversal(root.right, level+1, res)
            
        res = [[]]
        traversal(root, 0, res)
        return res
```
