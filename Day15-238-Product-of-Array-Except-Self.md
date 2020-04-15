<https://leetcode.com/problems/product-of-array-except-self/>

What we need to calculate is the product of every element except itself, in other words, the product of all elements on its left and its right. Therefore, we can iterate over the array twice, from left to right and from right to left respectively, and use cumulative products to record the products of all the elements on the left/right.

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        left_product = 1
        res = []
        for num in nums:
            res.append(left_product)
            left_product *= num
        right_product = 1
        for i in range(n-1, -1, -1):
            res[i] *= right_product
            right_product *= nums[i]
        return res
    
```



