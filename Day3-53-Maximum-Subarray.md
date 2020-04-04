<https://leetcode.com/problems/maximum-subarray/>

This is a classic Dynamic Programming problem: the maximum subarray ending at index `i`, is either `nums[i]` itself, or `nums[i]` plus the maximum subarray ending at index `i-1`,  based on either or not the latter value is positive or not. In other words, `f(i)` is equal to `nums[i]` unless `f(i-1)` is greater than 0 so that they add up to a larger value.  

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        if not nums:
            return 0
        dp = nums[0]
        res = dp
        for num in nums[1:]:
            if dp > 0:
                dp = dp + num
            else:
                dp = num
            res = max(res, dp)
        return res
```