<https://leetcode.com/problems/jump-game/>

This is a Greedy problem. All we need to do is iterate from the second last element and set the `dest` variable (initially set to `n-1`) to the index of it as long as it is available to jump to the `dest` from the position.

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        dest = n-1
        for i in range(n-2,-1,-1):
            if i + nums[i] >= dest:
                dest = i
        return dest==0
    
```

