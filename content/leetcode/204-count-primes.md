+++
date = "2021-02-26"
title = "204. Count primes"
tags = ["math"]
+++


Count the number of prime numbers less than a non-negative number, n.
Example:
Input: 10 Output: 4 Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.

- code, time limit exceeded
```py
class Solution:
    def countPrimes(self, n: int) -> int:
        if n < 2:
            return 0
        all_nums = list(range(2,n))
        # print(all_nums)
        index = 0
        while index < len(all_nums):
            cur = all_nums[index]
            # print('cur')
            # print(cur)
            # for i in range(2, n//cur + 1):
            for i in range(cur*cur, n, cur):
                # print('remove'+str(i))
                try:
                    # all_nums.remove(i*cur)
                    all_nums.remove(i)
                except ValueError:
                    pass
            index += 1
        # print(all_nums)
        return len(all_nums)

```
- code
```py
class Solution:
    def countPrimes(self, n: int) -> int:
        prime = [True] * n
        count = 0
        for num in range(2, n):
            if prime[num] == True:
                count += 1
                for i in range(num*num, n, num):
                    prime[i] = False
        return count

```
