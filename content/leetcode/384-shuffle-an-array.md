+++
date = "2021-02-21"
title = "384. Shuffle an array"
tags = ["design"]
+++

Shuffle a set of numbers without duplicates.
Implement the Solution class:

	Solution(int[] nums) Initializes the object with the integer array nums.
	int[] reset() Resets the array to its original configuration and returns it.
	int[] shuffle() Returns a random shuffling of the array.

- code0
```py
class Solution:

    def __init__(self, nums: List[int]):
        self.origin = nums[:]
        

    def reset(self) -> List[int]:
        """
        Resets the array to its original configuration and return it.
        """
        return self.origin
        

    def shuffle(self) -> List[int]:
        """
        Returns a random shuffling of the array.
        """
        nums = self.origin[:]
        random.shuffle(nums)
        return nums

```
- code1
```py
class Solution:
    def __init__(self, A):
        self.A = A
    def reset(self):
        '''
        Resets the array to its original configuration and return it.
        '''
        return list(self.A)
    def shuffle(self):
        '''
        Returns a random shuffling of the array.
        '''
        A = list(self.A)
        B = []
        while A:
            i  = random.randint( 0 , len(A) - 1 )
            A[i], A[-1] = A[-1], A[i]
            B.append( A.pop() )
        return B
```
- c2
```py
from random import shuffle

class Solution(object):

    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        self.original= list(nums)
        self.nums = nums
        
    def reset(self):
        """
        Resets the array to its original configuration and return it.
        :rtype: List[int]
        """
        return self.original
    
    def shuffle(self):
        """
        Returns a random shuffling of the array.
        :rtype: List[int]
        """
        
        temp = list(self.nums)
        
        for i in range(len(self.nums)):
            index = random.randrange(len(temp))
            # index = random.randint(0, leng-1)
            self.nums[i] = temp[index]
            del temp[index]
        return self.nums
```