<https://leetcode.com/problems/happy-number/>

The numbers that have appeared can be stored in a [Set](https://docs.python.org/3.7/library/stdtypes.html#set-types-set-frozenset) so that it can be checked if any number has appeared before.

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        existed = set()
        while n!= 1:
            if n in existed:
                return False
            else:
                existed.add(n)
                next_n = 0
                while n:
                    next_n += (n%10)**2
                    n = n // 10
                n = next_n
        return True
```

