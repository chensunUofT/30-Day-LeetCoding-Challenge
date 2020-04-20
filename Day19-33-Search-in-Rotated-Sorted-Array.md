<https://leetcode.com/problems/search-in-rotated-sorted-array/>

The idea is similar to the normal Binary Search, but the difference is that only half of the array is in order for this problem, so:
- If `nums[low] < nums[high]` (the left half is in order):
    - if `target` is in between, search in the left half (just like in normal Binary Search)
    - if `target` is not in between, search in the right half (since the left half is in order therefore `target` must not be in it)
- Vice versa

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        low, high = 0, len(nums) - 1
        while low <= high:
            if nums[low] == target:
                return low
            if nums[high] == target:
                return high
            mid = (low + high) // 2
            if target == nums[mid]:
                return mid
            if nums[low] <= nums[mid]:
                if nums[low] <= target < nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            else:
                if nums[mid] < target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1
        return -1
                 
```

