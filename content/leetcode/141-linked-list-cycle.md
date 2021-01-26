+++
date = "2021-01-26"
title = "141. Linked list cycle(T or F)"
tags = ["leetcode","linkedlist"]
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
```python
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
	bool hasCycle(ListNode *head) {
        if(head==NULL) return false;
        if(head->next == head) return true;
		while (head!=NULL&&head->val!=INT_MAX)
		{
			head->val = INT_MAX;
			head = head->next;
		}
        if(head) return true;
        else return false;
	}
};
```
