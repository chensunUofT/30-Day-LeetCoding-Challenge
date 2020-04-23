<https://leetcode.com/problems/subarray-sum-equals-k/>

The sum of a continuous subarray `k` is also the difference between two elements in the "cumulative sums" array; in other words, we need to find the occurrences when the differences between the "current cum sum" and a previous one equals `k`. In order to do that, we can use a hash table (or a Dictionary in Python) to store the frequencies of previous sums.

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        if not nums:
            return 0
        cum_sum = {0: 1}
        res = 0
        prev = 0
        for num in nums:
            cur = prev + num
            if cur - k in cum_sum:
                res += cum_sum[cur - k]
            if cur in cum_sum:
                cum_sum[cur] += 1
            else:
                cum_sum[cur] = 1
            prev = cur
        return res
 
```

