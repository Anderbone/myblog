+++
date = "2021-01-26"
title = "141. Linked list cycle(T or F)"
tags = ["linkedlist"]
+++

Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.

- code
```python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        quick = slow = head
        while quick and quick.next:
            quick = quick.next.next
            slow = slow.next
            if quick == slow:
                return True
        return False
```
- c java
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, quick = head;
        while (quick != null && quick.next != null){
            slow = slow.next;
            quick = quick.next.next;
            if (slow == quick){
                return true;
            }
        }
        return false;
    }
}
```



