+++
date = "2021-10-11"
title = "leetcode questions: BFS"
tags = ["leetcode","bfs","leetcode summary"]
toc = true
+++

### BFS Template
```java
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // store all nodes which are waiting to be processed
    Set<Node> visited;  // store all the nodes that we've visited
    int step = 0;       // number of steps neeeded from root to current node
    // initialize
    add root to queue;
    add root to visited;
    // BFS
    while (queue is not empty) {
        step = step + 1;
        // iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                if (next is not in used) {
                    add next to queue;
                    add next to visited;
                }
            }
            remove the first node from queue;
        }
    }
    return -1;          // there is no path from root to target
}
```

### [133. Clone graph](https://yanjiyu.com/leetcode/133/)
> Given a reference of a node in a **[connected](https://en.wikipedia.org/wiki/Connectivity_(graph_theory)#Connected_graph)** undirected graph.
Return a [deep copy](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) (clone) of the graph.
Each node in the graph contains a value (int) and a list (List[Node]) of its neighbors.
class Node { public int val; public List<Node> neighbors; }
```py
class Solution:
    def cloneGraph(self, node): # BFS 
        if not node:
            return node
        m = {node: Node(node.val)}
        deque = collections.deque([node])
        while deque:
            n = deque.popleft()
            for neigh in n.neighbors:
                if neigh not in m:
                    deque.append(neigh)
                    m[neigh] = Node(neigh.val)
                m[n].neighbors.append(m[neigh])
        return m[node]
```
### [752. open the lock](https://yanjiyu.com/leetcode/752/)
> You have a lock in front of you with 4 circular wheels. Each wheel has 10 slots: '0', '1', '2', '3', '4', '5', '6', '7', '8', '9'. The wheels can rotate freely and wrap around: for example we can turn '9' to be '0', or '0' to be '9'. Each move consists of turning one wheel one slot.
The lock initially starts at '0000', a string representing the state of the 4 wheels.
You are given a list of deadends dead ends, meaning if the lock displays any of these codes, the wheels of the lock will stop turning and you will be unable to open it.
Given a target representing the value of the wheels that will unlock the lock, return the minimum total number of turns required to open the lock, or -1 if it is impossible.  
**Example 1:**
Input: deadends = ["0201","0101","0102","1212","2002"], target = "0202" Output: 6 Explanation: A sequence of valid moves would be "0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202". Note that a sequence like "0000" -> "0001" -> "0002" -> "0102" -> "0202" would be invalid, because the wheels of the lock become stuck after the display becomes the dead end "0102".  
**Example 2:**
Input: deadends = ["8888"], target = "0009" Output: 1 Explanation: We can turn the last wheel in reverse to move from "0000" -> "0009".
```py
class Solution:
    def openLock(self, deadends: List[str], target: str) -> int:
        if "0000" in deadends:
            return -1
        queue = collections.deque()
        queue.append(('0000', 0))
        visited = set('0000')
        visited.update(deadends)
        
        while queue:
            string, step = queue.popleft()
            
            if string == target:
                return step
            
            for i in range(4):
                num = int(string[i])
                for dx in (-1, 1):
                    num_new = (num + dx) % 10
                    string_new = string[:i] + str(num_new) + string[i+1:]
                    if string_new not in visited:
                        queue.append((string_new, step+1))
                        visited.add(string_new)
        return -1

```
---
```py
class Solution:
    def openLock(self, deadends: List[str], target: str) -> int:
        if "0000" in deadends:
            return -1
        step = -1
        q = collections.deque(["0000"])
        visited = set("0000")
        visited.update(deadends)

        def findNeighbor(node):
            neighbors = []
            for i,v in enumerate(node):
                if v == "0":
                    l, r = "9", "1"
                elif v == "9":
                    l, r = "8", "0"
                else:
                    l, r = str(int(v)-1), str(int(v)+1)
                neighbors.append(node[:i] + l + node[i+1:])
                neighbors.append(node[:i] + r + node[i+1:])
            return neighbors

        while q:
            step += 1

            cur_q_size = len(q)
            while cur_q_size:
                cur_q_size -= 1
                cur = q.popleft()
                if cur == target:
                    return step
                neighbors = findNeighbor(cur)
                for neighbor in neighbors:
                    if neighbor not in visited:
                        q.append(neighbor)
                        visited.add(neighbor)

        return -1
```
### [279. Perfect squares](https://yanjiyu.com/leetcode/279/)
> Given an integer n, return __the least number of perfect square numbers that sum to__ n.
A perfect square is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, 1, 4, 9, and 16 are perfect squares while 3 and 11 are not.   
Example 1:
Input: n = 12 Output: 3 Explanation: 12 = 4 + 4 + 4.   
Example 2:
Input: n = 13 Output: 2 Explanation: 13 = 4 + 9.
```py
class Solution(object):
    def numSquares(self, n):
        candidates = collections.deque([0])
        visited = set()
        potential = [i*i for i in range(1, int(n**0.5) + 1)]
        step = 0
        while candidates:
            step += 1
            sz = len(candidates)
            for _ in range(sz):
                cur = candidates.popleft()
                for v in potential:
                    if v + cur < n and v + cur not in visited:
                        candidates.append(v + cur)
                        visited.add(v + cur)
                    elif v + cur == n:
                        return step
```
### [733. Flood fill](https://yanjiyu.com/leetcode/733/)
> CompaniesAn image is represented by an m x n integer grid image where image[i][j] represents the pixel value of the image.  
You are also given three integers sr, sc, and newColor. You should perform a **flood fill** on the image starting from the pixel image[sr][sc].  
To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with newColor.
Return __the modified image after performing the flood fill__.
```py
class Solution:
    def floodFill(self, image, sr, sc, newColor):
        old, m, n = image[sr][sc], len(image), len(image[0])
        if old != newColor: 
            q = collections.deque([(sr, sc)])
            while q:
                i, j = q.popleft()
                image[i][j] = newColor
                for x, y in ((i - 1, j), (i + 1, j), (i, j - 1), (i, j + 1)):
                    if 0 <= x < m and 0 <= y < n and image[x][y] == old: 
                        q.append((x, y))
        return image
```
[322. Coin Change](https://yanjiyu.com/leetcode/322-coin-change/)
> You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.
You may assume that you have an infinite number of each kind of coin.  
Example 1:
Input: coins = [1, 2, 5], amount = 11
Output: 3 Explanation: 11 = 5 + 5 + 1  
Example 2:
Input: coins = [2], amount = 3Output: -1
```py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        if amount == 0: return 0
        visited = set()
        potential = collections.deque(coins)
        visited.update(coins)
        step = 0
        
        while potential:
            step += 1
            for _ in range(len(potential)):
                if potential[0] == amount:
                    return step
                for c in coins:
                    if c + potential[0] not in visited:
                        potential.append(c + potential[0])
                        visited.add(c + potential[0])
                potential.popleft()
            if all(p > amount for p in potential):
                break
        return -1
```
---
```py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        if amount == 0: return 0
        queue = [[0, 0]]
        visited = {0}
        step = 0
        for node, step in queue:
            for coin in coins:
                if node + coin == amount: return step + 1
                elif node + coin < amount and node + coin not in visited:
                    queue.append([node + coin, step + 1])
                    visited.add(node + coin)
        return -1
```
### [542. 01-matrix](https://yanjiyu.com/leetcode/542/)
> Given an m x n binary matrix mat, return __the distance of the nearest __0__ for each cell__.
The distance between two adjacent cells is 1.   
**Example 1:**  
![](https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg)  
Input: mat = [[0,0,0],[0,1,0],[0,0,0]] Output: [[0,0,0],[0,1,0],[0,0,0]]
```py
class Solution:
    def updateMatrix(self, matrix):
        rows_len, cols_len = len(matrix), len(matrix[0])
        start_0 = [(x,y) for x in range(rows_len) for y in range(cols_len) if matrix[x][y] == 0]

        visited = set()
        q = deque(start_0)
        visited.update(start_0)
        # result = [[-1 for _ in range(cols_len)] for y in range(rows_len)]

        while q:
            for _ in range(len(q)):
                x, y = q.popleft()
                for d in [[0,1],[0,-1],[1,0],[-1,0]]:
                    m, n = x + d[0], y + d[1]
                    if 0 <= m < rows_len and 0 <= n < cols_len and (m,n) not in visited:
                        matrix[m][n] = matrix[x][y] + 1 # update matrix directly
                        q.append((m, n))
                        visited.add((m, n))
        
        return matrix
```
### [127. Word ladder](https://yanjiyu.com/leetcode/127/)
> A **transformation sequence** from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s1 -> s2 -> ... -> sk such that:  
Every adjacent pair of words differs by a single letter.
Every si for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.
sk == endWordGiven two words, beginWord and endWord, and a dictionary wordList, return __the **number of words** in the **shortest transformation sequence** from__ beginWord __to__ endWord__, or __0__ if no such sequence exists.__  
**Example 1:**  
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"] Output: 5 Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.
```py
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        
        def construct_dict(word_list):
            d = {}
            for word in word_list:
                for i in range(len(word)):
                    s = word[:i] + "_" + word[i+1:]
                    d[s] = d.get(s, []) + [word]
            return d
            
        def bfs_words(begin, end, dict_words):
            queue, visited = deque([(begin, 1)]), set()
            while queue:
                word, steps = queue.popleft()
                if word not in visited:
                    visited.add(word)
                    if word == end:
                        return steps
                    for i in range(len(word)):
                        s = word[:i] + "_" + word[i+1:]
                        neigh_words = dict_words.get(s, [])
                        for neigh in neigh_words:
                            if neigh not in visited:
                                queue.append((neigh, steps + 1))
            return 0
        
        d = construct_dict(set(wordList))
        return bfs_words(beginWord, endWord, d)
```