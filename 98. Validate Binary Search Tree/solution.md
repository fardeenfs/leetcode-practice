Here is my solution for the problem: [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)


## My Solution

```python
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


## My Solution (Same logic but easier to understand)

```python
def boundaryTraverse(root, minimum, maximum):
    if (root.val <= minimum or root.val >= maximum):
        return False
    
    if root.left:
        if (boundaryTraverse(root.left, minimum, root.val) ==  False):
            return False
        
    if root.right:
        if (boundaryTraverse(root.right, root.val , maximum) ==  False):
            return False
    
    return True

class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        return boundaryTraverse(root, float('-inf'), float('inf'))
        
```