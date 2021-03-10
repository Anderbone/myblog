+++ 
date = "2021-03-10"
title = "328. Odd even linked list"
tags = ["leetcode","linkedlist"]
+++


Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.
You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.
Example 1:
Input: 1->2->3->4->5->NULLOutput: 1->3->5->2->4->NULL

- code
```py
class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        if not head:
            return None
        flag = 0
        cur = head1 = head
        l2 = head2 = ListNode(0)
        cur = cur.next
        while cur:
            if flag == 1:
                head1.next = cur
                cur = cur.next
                head1 = head1.next
                flag = 0
              
            elif flag == 0:
                head2.next = cur
                cur = cur.next
                head2 = head2.next
                flag = 1
          
        head1.next = l2.next
        head2.next = None
        
        return head



```
- code
```py
class Solution:
    def oddEvenList(self, head):
        dummy1 = odd = ListNode(0)
        dummy2 = even = ListNode(0)
        while head:
            odd.next = head
            even.next = head.next
            odd = odd.next
            even = even.next
            head = head.next.next if even else None
        odd.next = dummy2.next
        return dummy1.next

```
