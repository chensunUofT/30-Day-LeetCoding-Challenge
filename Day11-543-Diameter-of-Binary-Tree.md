<https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/529/week-2/3293/>

Use DFS to find the depth of each sub-tree, and keep record of the length of the longest path, which is the sum of the depths of the two sub-trees.
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        
        def depth(tree):
            if not tree:
                return 0
            left_depth = depth(tree.left)
            right_depth = depth(tree.right)
            self.longest_path = max(self.longest_path, left_depth+right_depth)
            return 1 + max(left_depth, right_depth)
        
        if not root:
            return 0
        
        self.longest_path = 0
        depth(root)
        
        return self.longest_path
        
```
