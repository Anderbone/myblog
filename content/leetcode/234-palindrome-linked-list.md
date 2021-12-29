+++
date = "2021-01-25"
title = "234. Palindrome linked list"
tags = ["linkedlist"]
+++

Example 1:
Input: 1->2 Output: false
Example 2:
Input: 1->2->2->1 Output: true

- code, best
```python
def isPalindrome(self, head):
    rev = None
    slow = fast = head
    while fast and fast.next:
        fast = fast.next.next
        rev, rev.next, slow = slow, rev, slow.next
    if fast:
        slow = slow.next
    while rev and rev.val == slow.val:
        slow = slow.next
        rev = rev.next
    return not rev
```
- code, same, first by my own, reverse the left side slow link
```python
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        quick = slowhead = head
        slowpassed = None

        while quick and quick.next:
            quick = quick.next.next
            slowhead = head
            head = head.next
            slowhead.next = slowpassed
            slowpassed = slowhead
        
        if quick:
            head = head.next
        
        while head and slowpassed:
            if head.val != slowpassed.val:
                return False
            slowpassed, head = slowpassed.next, head.next
        if head or slowpassed:
            return False
        return True

```
- c
```python
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        if head is None:
            return True
        hare = turtle = curr = head
        while hare and hare.next:
            hare = hare.next.next
            turtle = turtle.next
        stack = []
        while turtle:
            stack.append(turtle.val)
            turtle = turtle.next
        while stack:
            if curr.val != stack.pop():
                return False
            curr = curr.next
        return True
```

