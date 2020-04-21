<https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/530/week-3/3306/>

The first idea is to use a binary search for each row and update the result as well as the right bond of the search area with the position of the first `1` in last row. The worst time complexity is `O(nlogm)`.

```python
# """
# This is BinaryMatrix's API interface.
# You should not implement it, or speculate about its implementation
# """
#class BinaryMatrix(object):
#    def get(self, x: int, y: int) -> int:
#    def dimensions(self) -> list[]:

class Solution:
    def leftMostColumnWithOne(self, binaryMatrix: 'BinaryMatrix') -> int:
        row, col = binaryMatrix.dimensions()
        res = col
        for i in range(row):
            low = 0
            high = res
            while low < high:
                mid = (low + high) // 2
                if binaryMatrix.get(i, mid):
                    res = mid
                    high = mid
                else:
                    low = mid + 1
        return res if res != col else -1
    
```

The second idea is to search from the top right corner:

- If the value is `1`, move to the left to see if there's another `1` on the left;
- If the value is `0`, then all the values to its left must be `0` as well, so we move down to see if there's `1` in another row.

The worst time complexity for this algorithm would be `O(m+n)`.

```python
# """
# This is BinaryMatrix's API interface.
# You should not implement it, or speculate about its implementation
# """
#class BinaryMatrix(object):
#    def get(self, x: int, y: int) -> int:
#    def dimensions(self) -> list[]:

class Solution:
    def leftMostColumnWithOne(self, binaryMatrix: 'BinaryMatrix') -> int:
        row, col = binaryMatrix.dimensions()
        res = -1
        i,j = 0, col-1
        while i < row and j >= 0:
            # print(i,j)
            if binaryMatrix.get(i, j):
                res = j
                j -= 1
            else:
                i += 1
        return res
    
```

