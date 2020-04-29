<https://leetcode.com/problems/binary-tree-maximum-path-sum/>

In this problem, what we want to find is the maximum value of the sum of all the nodes along a path, in other words, the value of the root node plus the two paths in left and right sub-trees. We can use a `max_path` global variable to store the maximum result and update it when a greater value is found.  
To find the longest path with current node being the "peak", use a `dfs` helper function to recurrently find the longest path starting at the left child and right child of the current node, and use the larger value between the "left path" and "right path" to determine the path (if it is greater than 0).

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    
    def maxPathSum(self, root: TreeNode) -> int:
        self.max_path = root.val
        self.dfs(root)
        return self.max_path
    
    def dfs(self, node):
        if not node:
            return 0
        left = max(self.dfs(node.left), 0)
        right = max(self.dfs(node.right), 0)
        self.max_path = max(self.max_path, node.val + left + right)
        return node.val + max(left, right)
        
```

