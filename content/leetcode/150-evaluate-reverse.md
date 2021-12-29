+++
date = "2021-04-06"
title = "150. Evaluate reverse polish notation"
tags = ["stack"]
+++


Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).
Valid operators are +, -, *, /. Each operand may be an integer or another expression.
Note:

 Division between two integers should truncate toward zero.
 The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.Example 1:
Input: ["2", "1", "+", "3", "*"] Output: 9 Explanation: ((2 + 1) * 3) = 9

- code, quicker
```py
class Solution():
    def evalRPN(self, tokens):

        intermediate_results = []
        OPERATORS = {
            '+': lambda y, x: x + y,
            '-': lambda y, x: x - y,
            '*': lambda y, x: x * y,
            '/': lambda y, x: int(x / y)
        }

        for token in tokens:
            if token in OPERATORS:
                intermediate_results.append(OPERATORS[token](
                    intermediate_results.pop(), intermediate_results.pop()))
            else:  # token is a number.
                intermediate_results.append(int(token))
        return intermediate_results[-1]



```
- code, quicker than using while and pop(0)
```py
class Solution():
    def evalRPN(self, tokens):
        stack = []
        for t in tokens:
            if t not in "+-*/":
                stack.append(int(t))
            else:
                r, l = stack.pop(), stack.pop()
                if t == "+":
                    stack.append(l+r)
                elif t == "-":
                    stack.append(l-r)
                elif t == "*":
                    stack.append(l*r)
                else:
                    stack.append(int(l/r))
        return stack.pop()



```
