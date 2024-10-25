Here is my solution for the problem: [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)


## Commented best solution from LC Solutions

```python
from collections import deque
from typing import List

class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        # Get the number of rows (m) and columns (n) in the grid
        m, n = len(grid), len(grid[0])
        
        # 'visited' is a reference to the original grid for modifying values
        visited = grid  
        q = deque()  # Initialize a queue to perform BFS
        countFreshOrange = 0  # Counter for fresh oranges

        # Loop through the grid to find rotten oranges and count fresh ones
        for i in range(m):
            for j in range(n):
                if visited[i][j] == 2:  # If the orange is rotten
                    q.append((i, j))  # Add its position to the queue
                if visited[i][j] == 1:  # If the orange is fresh
                    countFreshOrange += 1  # Increment the fresh orange count

        # If there are no fresh oranges initially, return 0 (no time needed)
        if countFreshOrange == 0:
            return 0
        
        # If there are no rotten oranges to start with and there are fresh oranges, return -1
        if not q:
            return -1
        
        minutes = -1  # Initialize minutes counter
        # Directions for moving right, left, down, and up
        dirs = [(1, 0), (-1, 0), (0, -1), (0, 1)]

        # Perform BFS until the queue is empty
        while q:
            size = len(q)  # Number of rotten oranges at the current level
            while size > 0:
                x, y = q.popleft()  # Get the position of the rotten orange
                size -= 1  # Decrease the size counter
                # Check all 4 possible directions for adjacent oranges
                for dx, dy in dirs:
                    i, j = x + dx, y + dy  # Calculate the position of the adjacent orange
                    # Check if the adjacent position is within bounds and is a fresh orange
                    if 0 <= i < m and 0 <= j < n and visited[i][j] == 1:
                        visited[i][j] = 2  # Rot the fresh orange
                        countFreshOrange -= 1  # Decrease the count of fresh oranges
                        q.append((i, j))  # Add the newly rotten orange to the queue
            minutes += 1  # Increment the minute counter after processing the current level
        
        # If all fresh oranges have rotted, return the number of minutes
        if countFreshOrange == 0:
            return minutes
        return -1  # If there are still fresh oranges left, return -1

    
```

