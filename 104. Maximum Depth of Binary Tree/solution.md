Here is my solution for the problem: [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)


## My Solution

```python
def maxDepth(root):
    if root == None:
        return 0
    left = maxDepth(root.left)
    right = maxDepth(root.right)
    return 1 + max(left, right)

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        return maxDepth(root)
    
```
