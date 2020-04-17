<https://leetcode.com/problems/number-of-islands/>

Use the idea of DFS to find every adjacent (in four directions) grid with value`'1'`, mark it as "visited" and increase the counter by 1 every time an "island" is completely explored.

```python
class Solution:
    
    def numIslands(self, grid: List[List[str]]) -> int:
        
        def dfs(grid, i, j):
            if grid[i][j] != '1':
                return grid
            grid[i][j] = 'v'
            if j > 0:
                dfs(grid, i, j - 1)
            if i > 0:
                dfs(grid, i - 1, j)
            if j < len(grid[0]) - 1:
                dfs(grid, i, j + 1)
            if i < len(grid) - 1:
                dfs(grid, i + 1, j)
        
        if not grid or not grid[0]:
            return 0
        row, col = len(grid), len(grid[0])
        count = 0
        for i in range(row):
            for j in range(col):
                if grid[i][j] == '1':
                    dfs(grid, i, j)
                    count += 1
        return count
           
```