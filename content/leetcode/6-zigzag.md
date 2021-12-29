+++
date = "2021-04-16"
title = "6. Zigzag"
tags = ["string"]
+++


The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
P A H N A P L S I I G Y I R 
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:
string convert(string s, int numRows);
Example 1:
Input: s = "PAYPALISHIRING", numRows = 3 Output: "PAHNAPLSIIGYIR" 
Example 2:
Input: s = "PAYPALISHIRING", numRows = 4 Output: "PINALSIGYAHRPI" Explanation: P I N A L S I G Y A H R P I

- code
```py
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1:
            return s
        # rows = [[]] * numRows  wrong way, append will apply to all sub-list
        rows = [[] for i in range(numRows)]
        flag = True
        step = 0
        for v in s:
            rows[step].append(v)

            if flag:
                if step == len(rows) - 1:
                    step -= 1
                    flag = False
                else:
                    step += 1
            else:
                if step == 0:
                    step += 1
                    flag = True
                else:
                    step -= 1
        
        return "".join([x for row in rows for x in row])

        # res = []
        # for row in rows:
        #     res.extend(row)
        # return "".join(res)



```
c
```py
class Solution:
    def convert(self, s: str, numRows: int) -> str:
		# below this check, code only works on 2 or more numRows
        if numRows < 2:
            return s
        # sets initial variables
        direction = 1
        row = 0
        output = ['']*numRows
        # loops through characters in strings
        for c in s:
            # adds current character to "row" in the array
            output[row] = output[row] + c
            # checks to see if at last available row (-1 because array starts at 0)
            if row == numRows-1:
                direction = -1
            # same as before just switches directions
            elif row == 0:
                direction = 1
            # next row is determined by direction positive or negative
            row += direction
        # returns the output list as a single string using nothing ('') as the "separator"
        return ''.join(output)
```
