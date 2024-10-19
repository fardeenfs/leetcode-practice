Here is my solution for the problem: [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)


## My Solution

```python
def levelOrderTraverse(root, depth, memo, memo_size):
    if root != None:
        if memo_size < depth:
            memo.append([root.val])
            memo_size += 1
        else:
            memo[depth-1].append(root.val)

        memo, memo_size = levelOrderTraverse(root.left, depth + 1, memo, memo_size)
        memo, memo_size = levelOrderTraverse(root.right, depth + 1, memo, memo_size)
    return memo, memo_size

class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        return levelOrderTraverse(root, 1, [], 0)[0] 
        
```


## BFS Solution (Slightly better memory complexity)

```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        # Iterative: BFS Level-Order 
        if not root:
            return []
        
        queue = collections.deque()
        level_order = []
        queue.append(root)

        while queue:
            level = []

            for _ in range(len(queue)):
                node = queue.popleft()
                level.append(node.val)

                if node.left:
                    queue.append(node.left)
                
                if node.right:
                    queue.append(node.right)

            level_order.append(level)

        return level_order

```