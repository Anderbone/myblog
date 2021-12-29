+++
date = "2021-03-12"
title = "105. Construct Binary Tree from Preorder and Inorder Traversal"
tags = ["tree"]
+++

Given preorder and inorder traversal of a tree, construct the binary tree.
Note:
You may assume that duplicates do not exist in the tree.
For example, given
preorder = [3,9,20,15,7] inorder = [9,3,15,20,7]
Return the following binary tree:
     3
   / \
  9  20
    /  \
   15   7

- code, 
```py
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if not inorder:
            return None
        root = TreeNode(preorder[0])
        root_index_inorder = inorder.index(preorder.pop(0))
        root.left = self.buildTree(preorder, inorder[:root_index_inorder])
        root.right = self.buildTree(preorder, inorder[root_index_inorder+1:])
        return root
        

```
why the input preorder doesn't need to be cut when we call the buildTree, since we only need to consider the root value to build the tree each time, and it's popped out in preorder list. The inorder index is correct, and when it's empty, we return None directly no matter what's in our preorder list.
- c
```py
class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if not inorder:
            return None
        d=len(inorder)-1
        i,j=0,d
        preorder.reverse()
        map_inorder={val:index for index,val in enumerate(inorder)}
        def recur(low,high):
            if low>high:
                return None
            root = TreeNode(preorder.pop())
            mid = map_inorder[root.val]
            root.left = recur(low,mid-1)
            root.right = recur(mid+1,high)
            return root

        return recur(0,d)
```
