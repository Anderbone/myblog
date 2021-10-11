+++
date = "2021-10-11"
title = "leetcode questions: DFS"
tags = ["leetcode","dfs","leetcode summary"]
+++

### DFS Templates
Template 1:
```java
/*
 * Return true if there is a path from cur to target.
 */
boolean DFS(Node cur, Node target, Set<Node> visited) {
    return true if cur is target;
    for (next : each neighbor of cur) {
        if (next is not in visited) {
            add next to visted;
            return true if DFS(next, target, visited) == true;
        }
    }
    return false;
}
```

Template 2 using an explicit stack to avoid stack overflow:
```java
/*
 * Return true if there is a path from cur to target.
 */
boolean DFS(int root, int target) {
    Set<Node> visited;
    Stack<Node> stack;
    add root to stack;
    while (s is not empty) {
        Node cur = the top element in stack;
        remove the cur from the stack;
        return true if cur is target;
        for (Node next : the neighbors of cur) {
            if (next is not in visited) {
                add next to visited;
                add next to stack;
            }
        }
    }
    return false;
}
```

### [200. Number of islands](https://yanjiyu.com/leetcode/200-number-of-islands/)
> Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.
Example 1:  
11110  
11010  
11000  
00000  
Output: 1 
```py
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        island = 0
        self.grid = grid
        self.m = len(grid[0])
        self.n = len(grid)

        for row in range(self.n):
            for col in range(self.m):
                cur = self.grid[row][col]
                if cur == "1":
                    island += 1
                    self.removeConnected(row, col)
        return island
    
    def removeConnected(self, row, col):
        self.grid[row][col] = "0"
        if col - 1 > -1 and self.grid[row][col-1] == "1":
            self.removeConnected(row, col-1)
        if col + 1 < self.m and self.grid[row][col+1] == "1":
            self.removeConnected(row, col+1)
        if row - 1 > -1 and self.grid[row-1][col] == "1":
            self.removeConnected(row-1, col)
        if row + 1 < self.n and self.grid[row+1][col] == "1":
            self.removeConnected(row+1, col)
```
### [133. Clone graph](https://yanjiyu.com/leetcode/133/)
> Given a reference of a node in a **[connected](https://en.wikipedia.org/wiki/Connectivity_(graph_theory)#Connected_graph)** undirected graph.
Return a [deep copy](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) (clone) of the graph.
Each node in the graph contains a value (int) and a list (List[Node]) of its neighbors.
class Node { public int val; public List<Node> neighbors; }
```py
class Solution:
    def cloneGraph(self, node): #DFS iteratively
        if not node:
            return node
        m = {node: Node(node.val)}
        stack = [node]
        while stack:
            n = stack.pop()
            for neigh in n.neighbors:
                if neigh not in m:
                    stack.append(neigh)
                    m[neigh] = Node(neigh.val)
                m[n].neighbors.append(m[neigh])
        return m[node]
```
```py
class Solution:
    def cloneGraph(self, node): # DFS recursively
        if not node:
            return node
        m = {node: Node(node.val)}
        self.dfs(node, m)
        return m[node]
    
    def dfs(self, node, m):
        for neigh in node.neighbors:
            if neigh not in m:
                m[neigh] = Node(neigh.val)
                self.dfs(neigh, m)
            m[node].neighbors.append(m[neigh])
```
### [733. Flood fill](https://yanjiyu.com/leetcode/733/)  
> CompaniesAn image is represented by an m x n integer grid image where image[i][j] represents the pixel value of the image.
You are also given three integers sr, sc, and newColor. You should perform a **flood fill** on the image starting from the pixel image[sr][sc].
To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with newColor.
Return __the modified image after performing the flood fill__.
```py
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        rows = len(image)
        cols = len(image[0])
        color_to_change = image[sr][sc]
        
        def dfs(r, c):
            
            if r < 0 or c < 0 or r>rows-1 or c>cols-1 or image[r][c]==newColor or image[r][c]!=color_to_change:
                return
            
            image[r][c] = newColor
            
            # radiate in four directions
            dfs(r+1,c)
            dfs(r-1,c)
            dfs(r,c+1)
            dfs(r,c-1)
        
        dfs(sr, sc)
        
        return image

```
Only dfs when it's an old color
```py 
class Solution:
    def floodFill(self, image, sr, sc, newColor):
        def dfs(i, j):
            image[i][j] = newColor
            for x, y in ((i - 1, j), (i + 1, j), (i, j - 1), (i, j + 1)):
                if 0 <= x < m and 0 <= y < n and image[x][y] == old:
                    dfs(x, y)
        old, m, n = image[sr][sc], len(image), len(image[0])
        if old != newColor: 
            dfs(sr, sc)
        return image
```