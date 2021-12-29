+++ 
date = "2020-12-28"
title = "Test for cyclicity"
tags = ["linkedlist"]
+++
takes the head of a singly linked list and returns null if there's no cycle.  
return the node at the start of the cycle if present
code
- code, a bit cheating, need to make sure there's no inf value before
```python
def has_cycle(head: ListNode) -> Optional[ListNode]:
    cur = head
    while cur:
        if cur.data == float('inf'):
            return cur
        cur.data = float('inf')
        cur = cur.next
    return None
```
- c2 if there's a cycle, fast and slow will meet. Starts from meet, meet--ans == head--ans.
```python
class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        meet = None
        fast = head
        slow = head
        # must check all 3 here
        while slow and  fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow is fast:
                meet = slow
                break
        
        if meet:
            p = head
            q = meet
            while p and q:
                if p is q:
                    return p
                p= p.next
                q = q.next
        return None
```

if the fast iterator jumps over the slow iterator, the slow iterator will equal the fast iterator in the next step.
- code ans
```python
def has_cycle(head: ListNode) -> Optional[ListNode]:
    def cycle_len(end):
        start, step = end, 0
        while True:
            step += 1
            start = start.next
            if start is end:
                return step

    fast = slow = head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next
        if slow is fast:
            # Finds the start of the cycle.
            cycle_len_advanced_iter = head
            for _ in range(cycle_len(slow)):
                cycle_len_advanced_iter = cycle_len_advanced_iter.next

            it = head
            # Both iterators advance in tandem.
            while it is not cycle_len_advanced_iter:
                it = it.next
                cycle_len_advanced_iter = cycle_len_advanced_iter.next
            return it  # iter is the start of cycle.
    return None  # No cycle.
```

