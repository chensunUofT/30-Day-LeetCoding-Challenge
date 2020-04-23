<https://leetcode.com/problems/bitwise-and-of-numbers-range/>

Note that the AND operation over the range would only keep those bits where it is `1` in every number in this range, otherwise it would be cancelled to `0` as long as there is any `0` in that bit in any number in the range. In other words, we need to find the a few "high" bits that are identical in all the numbers in the range, and fill the "low" bits with `0`.  
In order to do that, we can do right shifts on the upper and lower bounds of the range to remove the "low" bits until the two numbers become equal, and then do left shifts for the same number of times to fill the `0`'s.  
(Solution 1)

```python
class Solution:
    def rangeBitwiseAnd(self, m: int, n: int) -> int:
        if not m:
            return 0
        bit = 0
        while m != n:
            m >>= 1
            n >>= 1
            bit += 1
        return m << bit
    
```

Alternatively, we can iteratively do AND operation on `n`(the upper bound) with `n - 1`, which sets the last bit (when `n` is odd) or all the bits not higher than the lowest `1` (when `n` is even, e.g. 0b**1<u>100</u>**) to `0`, until the result is smaller or equal than the lower bound. The numbers skipped by the algorithm do not matter, because those alternating bits in these numbers would have already been set to `0`.  
(Solution 2)

```python
class Solution:
    def rangeBitwiseAnd(self, m: int, n: int) -> int:
        if not m:
            return 0
        while n > m:
            n &= n - 1
        return n
    
```

