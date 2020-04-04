<https://leetcode.com/problems/move-zeroes/>

Use one `fast` pointer to iterate over the array and assign the non-zero values to where another `slow` pointer is. When the `fast` pointer reaches the end, all the non-zero values are copied to the strat of the array, so we just need to assign `0` to the remaining part of the array.

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        if n < 2:
            return nums
        slow = 0
        for fast in range(n):
            if nums[fast]:
                nums[slow] = nums[fast]
                slow += 1
        while slow < n:
            nums[slow] = 0
            slow += 1
            
```



