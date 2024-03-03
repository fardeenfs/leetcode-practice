Here is my solution for the problem: [1319. Number of Operations to Make Network Connected](https://leetcode.com/problems/number-of-operations-to-make-network-connected/)


# Approach
Find number of connected components in the graph. If the number of connections is less than the minimum required to connect all nodes, return -1. Otherwise, count the number of connected components and subtract 1 to get the number of additional connections needed.

## My Solution

```python
class Solution:
    def makeConnected(self, n, connections):
        # Check if the number of connections is less than the minimum required to connect all nodes
        if len(connections) < n - 1:
            return -1  # It's not possible to connect all nodes
        
        # Initialize the graph as a list of empty sets, where each set represents connections for a node
        graph = [set() for _ in range(n)]
        for src, dest in connections:
            graph[src].add(dest)
            graph[dest].add(src)
        
        # Initialize a list to track whether each node has been visited
        visited = [False] * n
        
        # Define a function for depth-first search (DFS)
        def dfs(node):
            if visited[node]:
                return 0
            visited[node] = True
            for neighbor in graph[node]:
                dfs(neighbor)
            return 1
        
        # Perform DFS for each node and count the number of connected components
        connected_components = sum(dfs(i) for i in range(n))
        
        # Calculate and return the number of additional connections needed
        return connected_components - 1
```
