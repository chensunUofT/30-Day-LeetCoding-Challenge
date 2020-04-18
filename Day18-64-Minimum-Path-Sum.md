<https://leetcode.com/problems/minimum-path-sum/>

Given that the path is only allowed to go down or right, we can infer that, any point in the grid could only be reached from above or its left (if applicable), so the cost to that point is the cost for that grid itself plus **the minimum of the path sum to its top and left**.

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        for i in range(m):
            for j in range(n):
                if i == 0 and j == 0:
                    pass
                elif i == 0:
                    grid[i][j] += grid[i][j-1]
                elif j == 0:
                    grid[i][j] += grid[i-1][j]
                else:
                    grid[i][j] += min(grid[i][j-1], grid[i-1][j])
        return grid[-1][-1]
                
```

