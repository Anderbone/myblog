+++
date = "2021-03-11"
title = "160. Intersection of two linked lists"
tags = ["linkedlist"]
+++

Write a program to find the node at which the intersection of two singly linked lists begins.

- code
```py
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        def getLength(head):
            length = 0
            while head:
                head = head.next
                length += 1
            return length
        
        lena = getLength(headA)
        lenb = getLength(headB)
        if lena < lenb:
            headA, headB = headB, headA
        diff = getLength(headA) - getLength(headB)
        while diff:
            headA = headA.next
            diff -= 1
            
        if not headA or not headB:
            return None
        
        while headA != headB:
            headA, headB = headA.next, headB.next

        return headA

```
