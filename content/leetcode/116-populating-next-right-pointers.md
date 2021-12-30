+++ 
date = "2021-12-29"
title = "116. Populating Next Right Pointers in Each Node"
tags = ["binarytree"]
+++
[Populating Next Right Pointers in Each Node - LeetCode](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:
struct Node { int val; Node *left; Node *right; Node *next; } 
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.
Initially, all next pointers are set to NULL.
 
Example 1:
![](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)Input: root = [1,2,3,4,5,6,7] Output: [1,#,2,3,#,4,5,6,7,#] Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level. 
Example 2:
Input: root = [] Output: [] 
 
Constraints:

	The number of nodes in the tree is in the range [0, 212 - 1].
	-1000 <= Node.val <= 1000

---
- code ON, ON
```py
class Solution:
    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if not root: return None
        level = [root]
        while level:
            for i in range(len(level)-1):
                level[i].next = level[i+1]
            level = [i for node in level for i in (node.left, node.right) if i]
        return root 
```
- code ON, O1
```py
class Solution:
    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if not root: return root
        leftmost = root
        while leftmost.left:
            node = leftmost
            while node:
                node.left.next = node.right
                if node.next:
                    node.right.next = node.next.left
                node = node.next
            leftmost = leftmost.left
        return root
```
- code   ON, O1
```java

class Solution {
    public Node connect(Node root) {
        if (root == null) return root;
        Node leftmost = root;
        
        while(leftmost.left != null){
            Node node = leftmost;
            while(node.next != null){
                node.left.next = node.right;
                node.right.next = node.next.left;
                node = node.next;
            }
            node.left.next = node.right; // last node
            leftmost = leftmost.left;
        }
            
        return root;
    }
}
```
