+++
date = "2021-02-01"
title = "98. Validate binary search tree"
tags = ["leetcode","tree"]
+++

left < node < right is a valid binary search tree
Input: [2,1,3] Output: true
    2
   / \
  1   3

- code
```py
class Solution:
    # @param root, a tree node
    # @return a boolean
    # 7:38
    def isValidBST(self, root):
        output = []
        self.inOrder(root, output)
        
        for i in range(1, len(output)):
            if output[i-1] >= output[i]:
                return False

        return True

    def inOrder(self, root, output):
        if root is None:
            return
        
        self.inOrder(root.left, output)
        output.append(root.val)
        self.inOrder(root.right, output)

```
- code
```py
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        def inorder(node):
            if node:
                nonlocal res
                inorder(node.left)
                if node.val <= res:
                    nonlocal flag
                    flag = False
                    return
                res = node.val
                inorder(node.right)

        flag = True
        res = float('-inf')
        inorder(root)
        return flag

```
