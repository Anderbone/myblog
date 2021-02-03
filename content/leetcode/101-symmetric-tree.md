+++
date = "2021-02-03"
title = "101. Symmetric tree"
tags = ["leetcode","tree"]
+++


Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
     1
   / \
  2   2
 / \ / \
3  4 4  3
 
But the following [1,2,2,null,3,null,3] is not:
     1
   / \
  2   2
   \   \
   3    3

- code better
```py
class Solution:
    def isSymmetric(self, root):
        def isSym(L,R):
            if not L and not R: return True
            if L and R and L.val == R.val: 
                return isSym(L.left, R.right) and isSym(L.right, R.left)
            return False
        return isSym(root, root)

```
- code, check each level.
```py
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        def checkBalance(eachList):
            for i in range(len(eachList) // 2):
                if not eachList[i] and not eachList[-i-1]:
                    continue
                if not eachList[i] or not eachList[-i-1]:
                    return False
                if eachList[i].val != eachList[-i-1].val:
                    return False
            return True

        level = [root]
        while level:
            if all(x is None for x in level):
                break
            if not checkBalance(level):
                return False
            newlevel = []
            for n in level:
                if not n:
                    next = (None, None)
                elif n.left and not n.right:
                    next = (n.left, None)
                elif n.right and not n.left:
                    next = (None, n.right)
                else:
                    next = (n.left, n.right)
                for i in next:
                    newlevel.append(i)
            level[:] = newlevel
        return True

```
