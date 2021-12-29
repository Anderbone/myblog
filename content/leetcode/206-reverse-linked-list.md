+++
date = "2021-01-21"
title = "206. Rotate array"
tags = ["linkedlist"]
+++

Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL

- code best
```python
    def reverseList(self, head):
        prev = None
        curr = head

        while curr:
            next = curr.next
            curr.next = prev
            prev = curr
            curr = next
        
        return prev

```
- code own
```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        if not head.next.next:
            head.next.next = head
            res = head.next
            head.next = None
            return res
        
        first, second, third = head, head.next, head.next.next
        first.next = None
        while second:
            second.next = first
            if not third:
                return second
            first, second, third = second, third, third.next

```
- c old
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if head is None:
            return None
        
        if head.next is None:
            return head
            
        pre = head
        first = pre
        second = pre.next
        if second.next is None:
            first.next = None
            second.next = first
            return second
        pre = second.next
        count = 0
        while(True):
            second.next = first
            if count == 0:
                first.next = None
                count += 1
            first = second
            second = pre
            if pre.next is None:
                break
            pre = pre.next
        second.next = first
        return second
```
