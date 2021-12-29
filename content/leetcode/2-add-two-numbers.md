+++
date = "2021-03-10"
title = "2. Add two numbers"
tags = ["linkedlist"]
+++



You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.
Example:
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4) Output: 7 -> 0 -> 8 Explanation: 342 + 465 = 807.


Don't forget to handle the possible extra carry, e.g. 
Testcase   
[9,9,9,9,9,9,9]  
[9,9,9,9]  
Answer   [8,9,9,9,0,0,0]  
Expected Answer  [8,9,9,9,0,0,0,1]

- code
```py
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carry = 0
        res = head = ListNode(0)
        while l1 or l2:
            num1 = num2 = 0
            if l1:
                num1 = l1.val
                l1 = l1.next
            if l2:
                num2 = l2.val
                l2 = l2.next
            summ = num1 + num2 + carry
            carry = summ // 10
            cur = summ % 10
            head.next = ListNode(cur)
            head = head.next
        if carry:
            head.next = ListNode(carry)
        return res.next



```
- code slow
```py
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        def getNum(l):
            num = n = 0
            while l:
                num = num + l.val * (10**n)
                l = l.next
                n += 1
            return num
        
        num1 = getNum(l1)
        num2 = getNum(l2)

        summ = num1 + num2
        l_sum = list(str(summ))
        lastNode = None
        for i in l_sum:
            cur = ListNode(i)
            cur.next = lastNode
            lastNode = cur
        return cur

```
