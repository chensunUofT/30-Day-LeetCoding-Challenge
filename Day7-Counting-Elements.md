<https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/528/week-1/3289/>



Use a set to record all the "minus-one" values of the elements in the original array, and count the elements if appear in the `minus_one_set`.

```python
class Solution:
    def countElements(self, arr: List[int]) -> int:
        minus_one_set = set([num-1 for num in arr])
        cnt = [num in minus_one_set for num in arr]
        return sum(cnt)
    
```



