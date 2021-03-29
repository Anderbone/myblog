
+++
date = "2021-03-29"
title = "297. Serialize and Deserialize Binary Tree"
tags = ["leetcode","design"]
+++


Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.
Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

You may serialize the following tree:

    1  
   / \  
  2   3  
     / \  
    4   5  
as "[1,2,3,null,null,4,5]"



- code
```py
class Codec:

    def serialize(self, root):
        def doit(node):
            if node:
                vals.append(str(node.val))
                doit(node.left)
                doit(node.right)
            else:
                vals.append('#')
        vals = []
        doit(root)
        return ' '.join(vals)

    def deserialize(self, data):
        def doit():
            val = next(vals)
            if val == '#':
                return None
            node = TreeNode(int(val))
            node.left = doit()
            node.right = doit()
            return node
        vals = iter(data.split())
        return doit()

```
- c list  1,2,*,*,3,4,*,*,5,*,*
```py
class Codec:
    def serialize(self, root):
       
        def helper(node):
            if node:
                res.append(str(node.val))
                helper(node.left)
                helper(node.right)
            else:
                res.append("#")
            
        res = []
        helper(root)
        return " ".join(res)
            

    def deserialize(self, data):
       
        def helper(datalist):
            if datalist[0] == "#":
                datalist.popleft()
                return None
            
            root = TreeNode(datalist[0])
            datalist.popleft()
            root.left = helper(datalist)
            root.right = helper(datalist)
            return root 
        
        data = collections.deque(data.split())
        root = helper(data)
        return root
```
