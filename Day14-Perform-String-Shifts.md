<https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/529/week-2/3299/>

Note that the left shift and right shift cancel each other, we can firstly calculate the total shift from the whole matrix and then do the operation only once. Two more things to mention when shifting:

1. Shifting to left/right by `k` is equivalent to shifting by `k % n` where n is the length of the string;
2. Shifting to right by `k` is equivalent to shifting to left by `-k` or `n - k` or `-k % n`;

Therefore, we use a `k` variable to store the amount of shifting to left after being cancelled by right:

- If it is positive, we just need to left-shift by `k % n`;
- If it is negative, it means we need to right-shift by `-k` , or left-shift by `-(-k) % n` which is also `k % n`

Afterall, whatever the `k` value is, all we need to do is left-shift the string by `k % n`.

```python
class Solution:
    def stringShift(self, s: str, shift: List[List[int]]) -> str:
        
        n = len(s)
        if n < 2:
            return n
        
        k = 0
        for (direction, amount) in shift:
            if not direction:
                k += amount
            else:
                k -= amount

        k %= n
        return s[k:] + s[:k]

```



