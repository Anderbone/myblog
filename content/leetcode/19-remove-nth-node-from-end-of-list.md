+++
date = "2021-01-19"
title = "Remove Nth node from end of list"
tags = ["leetcode","linkedlist"]
+++

Example:
Given linked list: 1->2->3->4->5, and n = 2. After removing the second node from the end, the linked list becomes 1->2->3->5.

- c1 dump head
```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dumphead = ListNode(0, head)
        count = head
        leng = 0

        while count:
            count = count.next
            leng += 1

        target_before = leng - n

        # delete head
        if target_before == 0:
            head = head.next
            return head

        while target_before > 0:
            dumphead = dumphead.next
            target_before -= 1

        dumphead.next = dumphead.next.next

        return head

```
- c0 old
```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        if head.next is None:
            return None
        
        count = 0
        pre = ListNode(0)
        pre.next = head
        while(pre.next is not None):
            pre = pre.next
            count += 1

        pre2 = head
        ans = pre2
  
        if n == 1:
            while(count != 2):
                count -= 1
                pre2 = pre2.next
            pre2.next = None
                
        else:
            while(count != n):
                count -= 1
                pre2 = pre2.next
            pre2.val = pre2.next.val 
		# must val first, then next
            pre2.next = pre2.next.next
        return ans
```
