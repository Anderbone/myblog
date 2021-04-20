+++ 
date = "2021-04-20"
title = "142. Linked list cycle II"
tags = ["leetcode","linkedlist"]
+++


Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.

- c   f there's a cycle, fast and slow will meet. Starts from meet, meet--ans == head--ans.
```py
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
                
H = head - ans,  D = meet - ans, L = cycle
If fast and slow both start at head, when fast catches slow, slow has traveled H+D and fast 2(H+D).  Fast traveled more nL than slow.
Assume fast has traveled n loops in the cycle, we have:
2H + 2D = H + D + nL  -->  H + D = nL  --> H = nL - D
- code
```py
class Solution:
    # @param head, a ListNode
    # @return a list node
    def detectCycle(self, head):
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                slow2 = head
                while slow != slow2:
                    slow = slow.next
                    slow2 = slow2.next
                return slow

```
