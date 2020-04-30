<https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/532/week-5/3315/>

To check if the array is "valid" with the binary tree:

- The value in the array must be equal to the corresponding value in the tree
- Either of the sub-trees has to follow the same rule with the next value in the array
- If the end of the array is reached, the corresponding node must be a leaf node, i.e. both of its children have to be empty.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right


class Solution:
    
    def isValidSequence(self, root: TreeNode, arr: List[int]) -> bool:
        if not arr:
            return not root
        self.nums = arr
        self.n = len(arr)
        return self.dfs(root, 0)
        
    def dfs(self, node, pos):
        if not node or node.val != self.nums[pos]:
            return False
        if pos == self.n - 1:
            return not (node.left or node.right)
        return self.dfs(node.left, pos + 1) or self.dfs(node.right, pos + 1)
        
```

