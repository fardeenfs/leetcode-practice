Here is my solution for the problem: [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)


## My Solution

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []

        def inOrder(root):
            if root:
                # First recur on left child
                inOrder(root.left)
                # Then print the data of node
                result.append(root.val)
                # Now recur on right child
                inOrder(root.right)

        inOrder(root)
        return(result) 

```
