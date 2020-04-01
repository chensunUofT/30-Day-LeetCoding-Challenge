If we do a [bit-wise XOR operation](https://en.wikipedia.org/wiki/Bitwise_operation#XOR) on the whole array, every pair of duplicate elements is cancelled since `x XOR x == 0` for every number x. Therefore, the result of the XOR operation is the only single number.

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0
        for num in nums:
            res ^= num
        return res
```

Alternatively, to make it one-line,  we can use [reduce](https://docs.python.org/3/library/functools.html#functools.reduce):

```python
from functools import reduce

class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        return reduce((lambda x,y: x ^ y), nums)
```

