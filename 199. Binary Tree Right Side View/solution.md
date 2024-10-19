Here is my solution for the problem: [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)


## My Solution (DFS - Recursive Solution)

```python
def rightFirstTraverse(root, depth, right_side, size):
    if root != None:
        if depth > size:
            right_side.append(root.val)
            size += 1
        right_side, size = rightFirstTraverse(root.right, depth + 1, right_side, size)
        right_side, size = rightFirstTraverse(root.left, depth + 1, right_side, size)
    return right_side, size

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        return rightFirstTraverse(root, 1, [], 0)[0]

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

