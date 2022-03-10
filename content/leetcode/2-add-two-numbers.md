+++ 
date = "2022-03-10"
title = "2. Add Two Numbers"
tags = ["linkedlist"]
+++
https://leetcode.com/problems/add-two-numbers/

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.
Example:
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4) Output: 7 -> 0 -> 8 Explanation: 342 + 465 = 807.
---
- code
```py
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carry = 0
        result_tail = result = ListNode(0)
        while l1 or l2 or carry:
            l1v = l1.val if l1 else 0
            l2v = l2.val if l2 else 0
            carry, out = divmod(l1v + l2v + carry, 10)
            result_tail.next = ListNode(out)
            result_tail = result_tail.next
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
        return result.next

```
