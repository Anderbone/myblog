+++
date = "2021-03-13"
title = "116. Populating Next Right Pointers in Each Node"
tags = ["tree"]
+++

You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:
struct Node { int val; Node *left; Node *right; Node *next; } 
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.
Initially, all next pointers are set to NULL.

- code
```py
class Solution:
    def connect(self, root):
        res = root
        while root and root.left:
            next = root.left
            while root:
                root.left.next = root.right
                root.right.next = root.next and root.next.left
                root = root.next
            root = next
        return res

```
- code
```py
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        if not root:
            return None
        thislevel = [root]
        while thislevel:
            for i in range(len(thislevel)):
                if i == len(thislevel)-1:
                    thislevel[i].next = None
                else:
                    thislevel[i].next = thislevel[i+1]
            thislevel = [i for node in thislevel for i in (node.left, node.right) if i]
        return root

```
- code
```py
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        
        def levelOrder(root: TreeNode) -> List[List[int]]:
            if not root:
                return []

            def traversal(root, level, res):
                if not root:
                    return
                if len(res) <= level:
                    res.append([])
                res[level].append(root)
                traversal(root.left, level+1, res)
                traversal(root.right, level+1, res)

            res = [[]]
            traversal(root,0,res)
            return res
        
        res = levelOrder(root)
        
        for level,row in enumerate(res):
            for count,each in enumerate(row):
                if count == 2**level-1:
                    each.next = None
                else:
                    # while(each is not None):
                    each.next = row[count+1]
        return root
```
