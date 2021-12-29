+++
date = "2021-01-19"
title = "237. Delete a node in a linked list"
tags = ["linkedlist"]
+++

Input: head = [4,5,1,9], node = 5
Output: [4,1,9]

- c
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
```
