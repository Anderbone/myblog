+++
date = "2021-01-28"
title = "104. Maximum depth of binary tree"
tags = ["tree"]
+++

3  
/ \    
9  20  
/   \  
15   7  
return its depth = 3.

- code0
```python
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))

```
- c1 iteration
```python
class Solution:
    def maxDepth(self, root):
        if not root: return 0 
        level = [root]; depth = 0
        while level:
            depth += 1
            level = [i for n in level for i in (n.left, n.right) if i]
        return depth
```

