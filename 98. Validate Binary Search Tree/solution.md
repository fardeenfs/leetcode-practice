Here is my solution for the problem: [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)


## My Solution

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
        
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        result = []
        
        def traverse(root, low, high):
            if not root:
                return True
            elif not low < root.val < high:
                return False
            return traverse(root.left,low, root.val) and traverse(root.right,root.val, high)
        return traverse(root,low=float('-inf'), high=float('inf'))
```
