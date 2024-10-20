Here is my solution for the problem: [222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/)


## My Solution

```python
def left_right_traverse(root, depth):
    if root is None:
        return 0

    # Count left depth
    left_depth = 0
    curr = root.left
    while curr:
        left_depth += 1
        curr = curr.left
    
    # Count right depth
    right_depth = 0
    curr = root.right
    while curr:
        right_depth += 1
        curr = curr.right

    # If left depth equals right depth, it's a full tree
    if left_depth == right_depth:
        return (1 << (left_depth + 1)) - 1  # 2^(left_depth + 1) - 1

    # Recur for left and right subtrees
    left_count = left_right_traverse(root.left, depth + 1)
    right_count = left_right_traverse(root.right, depth + 1)

    return left_count + right_count + 1

class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0
        return left_right_traverse(root, 1)
    
```
