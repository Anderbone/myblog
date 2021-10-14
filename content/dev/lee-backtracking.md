+++
date = "2021-10-11"
title = "leetcode questions: Backtracking"
tags = ["leetcode","backtracking","leetcode summary","dfs"]
toc = true
+++

### Template
```py
def backtrack(candidate):
    if find_solution(candidate):
        output(candidate)
        return
    
    # iterate all possible candidates.
    for next_candidate in list_of_candidates:
        if is_valid(next_candidate):
            # try this partial candidate solution
            place(next_candidate)
            # given the candidate, explore further.
            backtrack(next_candidate)
            # backtrack
            remove(next_candidate)
```
 ### [17. Letter Combinations of a Phone Number ](https://yanjiyu.com/leetcode/17-letter-combinations-of-a-phone/)
 > Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.  
A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.  
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```py
class Solution(object):
    def letterCombinations(self, digits):
        def backTracking(digits, carry):
            if digits == []:
                res.append(carry)
                return

            number = digits[0]
            for j in dic[number]:
                backTracking(digits[1:], carry + j)
                 
        if not digits:
            return []
        digits = list(digits)
        res = []
        dic = {'2': "abc", '3': "def", '4': "ghi", '5': "jkl", '6': "mno", '7': "pqrs", '8': "tuv", '9': "wxyz"}
        backTracking(digits, '')
        return res
```
### [22. Generate Parentheses](https://yanjiyu.com/leetcode/22/)
> Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
For example, given n = 3, a solution set is:
[ "((()))", "(()())", "(())()", "()(())", "()()()" ]
```py
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        def backtracking(temp, left, right):
            if len(temp) == 2 * n:
                ans.append(temp)
                return 
                
            if left < n:
                backtracking(temp+'(', left+1, right)
            if right < left:
                backtracking(temp+')', left, right+1)

        ans = []
        backtracking('', 0, 0)
        return ans
```
### [46 Permutations](https://yanjiyu.com/leetcode/46/)
> Given an array nums of distinct integers, return __all the possible permutations__. You can return the answer in **any order**.  
Input: [1,2,3]  
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
 ```py
   def permute(self, nums: List[int]) -> List[List[int]]:
        def dfs(nums, permutation, result):
            if nums == []:
                result.append(permutation)
            for i,x in enumerate(nums):
                dfs(nums[:i] + nums[i+1:], permutation + [x], result)
            
        result = []
        dfs(nums, [], result)
        return result
```
### [78. subsets](https://yanjiyu.com/leetcode/78-subset/)
> Given a set of distinct integers, nums, return all possible subsets (the power set).
Note: The solution set must not contain duplicate subsets.
Example:
Input: nums = [1,2,3] Output: [ [3],   [1],   [2],   [1,2,3],   [1,3],   [2,3],   [1,2],   [] ]
```py
class Solution:
    def subsets(self, nums):
        res = []
        def dfs(nums, path, res):
            res.append(path)
            for i,v in enumerate(nums):
                # dfs(nums[:i]+nums[i+1:], res, path+[v]) no duplicate
                dfs(nums[i+1:], path+[v], res)
        dfs(nums, [], res)
        return res
```
### [79. Word Search](https://yanjiyu.com/leetcode/79-word-search/)
> Given a 2D board and a word, find if the word exists in the grid.
The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.
Example:
board = [ ['A','B','C','E'], ['S','F','C','S'], ['A','D','E','E'] ] Given word = "ABCCED", return true. Given word = "SEE", return true. Given word = "ABCB", return false
```py
class Solution:
    
    def exist(self, board: List[List[str]], word: str) -> bool:

        count = collections.Counter(x for rows in board for x in rows)
        for c, cnt in collections.Counter(word).items():
            if cnt > count[c]:
                return False

        self.res = False
        self.word = word
        self.width = len(board[0])
        self.height = len(board)
        start_points = [(row,col) for row in range(self.height) 
        for col in range(self.width) if board[row][col] == word[0]]

        for x, y in start_points:
            board[x][y] = ""
            self.dfs(board, 1, x, y) # word[1] is next target
            board[x][y] = word[0]
        return self.res

    def dfs(self, board, word_index, x, y):
        if word_index == len(self.word):
            self.res = True
            return
        if x < 0 or y < 0 or x == self.height or y == self.width:
            return
        
        if x-1 >= 0 and board[x-1][y] == self.word[word_index]:
            board[x-1][y] = ""
            self.dfs(board, word_index+1, x-1, y)
            board[x-1][y] = self.word[word_index]
        
        if y-1 >= 0 and board[x][y-1] == self.word[word_index]:
            board[x][y-1] = ""
            self.dfs(board, word_index+1, x, y-1)
            board[x][y-1] = self.word[word_index]
        
        if x+1 < self.height and board[x+1][y] == self.word[word_index]:
            board[x+1][y] = ""
            self.dfs(board, word_index+1, x+1, y)
            board[x+1][y] = self.word[word_index]
        
        if y+1 < self.width and board[x][y+1] == self.word[word_index]:
            board[x][y+1] = ""
            self.dfs(board, word_index+1, x, y+1)
            board[x][y+1] = self.word[word_index]
```
---
```py
class Solution:
    
    def exist(self, board: List[List[str]], word: str) -> bool:
        count = collections.Counter(x for rows in board for x in rows)
        for c, cnt in collections.Counter(word).items():
            if cnt > count[c]:
                return False
            
        r = len(board)
        c = len(board[0])
        length = len(word)
        
        def go(x, y, index):
            if index == length:
                return True
            
            w = word[index]
            
            prev = board[x][y]
            board[x][y] = '' 
            
            if x > 0 and board[x - 1][y] == w and go(x - 1, y, index + 1):
                return True
            if x + 1 < r and board[x + 1][y] == w and go(x + 1, y, index + 1):
                return True
            if y > 0 and board[x][y - 1] == w and go(x, y - 1, index + 1):
                return True
            if y + 1 < c and board[x][y + 1] == w and go(x, y + 1, index + 1):
                return True
            
            board[x][y] = prev
            return False
        
        candidates = [(x, y) for x in range(r) for y in range(c) if board[x][y] == word[0]]
        
        return any(go(x, y, 1) for x, y in candidates)
```
### [47. Permutations-II](https://yanjiyu.com/leetcode/47/)
> Given a collection of numbers, nums, that might contain duplicates, return __all possible unique permutations **in any order**.__  
**Example 1:**
Input: nums = [1,1,2] Output: [[1,1,2], [1,2,1], [2,1,1]]  
**Example 2:**
Input: nums = [1,2,3] Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```py
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        def dfs(nums, cur, res):
            if not nums:
                res.append(cur)
                return

            visited = set()
            for i,num in enumerate(nums):
                if num not in visited:
                    visited.add(num)
                    # cur.append(num) wrong position to update!
                    dfs(nums[:i]+nums[i+1:], cur+[num], res)

        res = []
        dfs(nums, [], res)
        return res

```