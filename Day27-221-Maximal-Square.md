<https://leetcode.com/problems/maximal-square/>

Use a 2-D array `dp[i][j]` (with the same size of the input matrix) to represent the length (of one side) of the largest square in the matrix whose bottom-right corner is at position `(i,j)`. If the element at the position is `'0'`, then the value in the dp memorization matrix shoule be `0`; If position `(i,j)` is on the top or left edge, there is no way to find a square larger than 1, so it just depends on the value of the element as well; **otherwise, `dp[i][j]` would depend on its top, left and top-left**: it shoube be set to one plus the minimum value of those three, considering that a square with length `x` and bottom-right corner at index `(i,j)` would "include" three squares with length `x-1` on the top, left and top-left directions of the corner point.

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if not matrix or not matrix[0]:
            return 0
        res = 0
        row, col = len(matrix), len(matrix[0])
        dp = [[0 for _ in range(col)] for _ in range(row)]
        for i in range(row):
            for j in range(col):
                if i == 0 or j == 0:
                    dp[i][j] = int(matrix[i][j] == '1')
                else:
                    if matrix[i][j] == '1':
                        dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
                res = max(res, dp[i][j])
        return res ** 2
    
```

The space complexity of the previous solution is `O(mn)`, but it can be optimized to `o(n)` since we only need the upper row and the value to its left in the `dp` matrix when calculating for each point. Thus, a 1-D array of length `n` and a `dp_left` variable are enough.

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if not matrix or not matrix[0]:
            return 0
        res = 0
        row, col = len(matrix), len(matrix[0])
        dp_prev_row = [0 for _ in range(col)]
        for i in range(row):
            dp_left = int(matrix[i][0] == '1')
            res = max(res, dp_left)
            dp_cur_row = [dp_left]
            for j in range(1, col):
                if matrix[i][j] == '0':
                    dp_cur = 0
                else:
                    dp_cur = 1 + min(dp_left, dp_prev_row[j-1], dp_prev_row[j])
                    res = max(res, dp_cur)
                dp_cur_row.append(dp_cur)
                dp_left = dp_cur
            dp_prev_row = dp_cur_row
        return res ** 2
            
```



