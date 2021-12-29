+++
date = "2021-03-11"
title = "94. Binary tree inorder traversal"
tags = ["tree"]
+++

Given a binary tree, return the inorder traversal of its nodes' values.

- code
```py
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        def inorder(node):
            if not node:
                return
            inorder(node.left)
            res.append(node.val)
            inorder(node.right)
        inorder(root)
        return res

```
- c iterative
```py
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res, stack = [], []
        while True:
            while root:
                stack.append(root)
                root = root.left
            if not stack: return res
            node = stack.pop()
            res.append(node.val)
            root = node.right
```
