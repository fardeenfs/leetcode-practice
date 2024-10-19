Here is my solution for the problem: [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)


## My Solution (DFS - Recursive Solution)

```python
def rightFirstTraverse(root, depth, right_side):
    if root != None:
        if depth > len(right_side):
            right_side.append(root.val)
        right_side = rightFirstTraverse(root.right, depth + 1, right_side)
        right_side = rightFirstTraverse(root.left, depth + 1, right_side)
    return right_side

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        return rightFirstTraverse(root, 1, [])

```


## Another Solution (BFS - Iterative Solution)

```python
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if(root is None):
            return []
        queue = deque([root])
        res = []
        while(len(queue) > 0):
            for _ in range(len(queue)):
                node = queue.popleft()
                if(node.left is not None):
                    queue.append(node.left)
                if(node.right is not None):
                    queue.append(node.right)
            res.append(node.val)
        return res

```

