+++ 
date = "2020-12-28"
title = "Merge two sorted list"
tags = ["linkedlist"]
+++
c
```
def merge_two_sorted_lists(L1, L2):

    # Creates a placeholder for the result.
    dummy_head = tail = ListNode()

    while L1 and L2:
        if L1.data < L2.data:
            tail.next, L1 = L1, L1.next
        else:
            tail.next, L2 = L2, L2.next
        tail = tail.next

    # Appends the remaining nodes of L1 or L2
    tail.next = L1 or L2
    return dummy_head.next
```
remember to use two pointer, one move, one for return
