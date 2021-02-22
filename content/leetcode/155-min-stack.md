+++
date = "2021-02-22"
title = "155. Min Stack"
tags = ["leetcode","design"]
+++

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

	push(x) -- Push element x onto stack.
	pop() -- Removes the element on top of the stack.
	top() -- Get the top element.
	getMin() -- Retrieve the minimum element in the stack.
c
- code, one stack, save the min at each time at the second place, for e.g. input (1,3,-2) will become (1,1),(3,1)(-2,-2)
```py
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack= []

    def push(self, x):
        """
        :type x: int
        :rtype: nothing
        """
        if not self.stack:self.stack.append((x,x)) 
        else:
            self.stack.append((x,min(x,self.stack[-1][1])))

    def pop(self):
        """
        :rtype: nothing
        """
        if self.stack: self.stack.pop()

    def top(self):
        """
        :rtype: int
        """
        if self.stack: return self.stack[-1][0]
        else: return None

    def getMin(self):
        """
        :rtype: int
        """
        if self.stack: return self.stack[-1][1]
        else: return None

```
- c two stacks
```py
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.min_stack = []
        self.stack = []
        

    def push(self, x: int) -> None:
        self.stack.append(x)
        if not self.min_stack or x <= self.min_stack[-1]:
            self.min_stack.append(x)

    def pop(self) -> None:
        ele = self.stack.pop()
        if ele == self.min_stack[-1]:
            self.min_stack.pop()
        return ele
        

    def top(self) -> int:
        return self.stack[-1]
        
    def getMin(self) -> int:
        return self.min_stack[-1]
```
