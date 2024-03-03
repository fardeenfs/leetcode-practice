Here is my solution for the problem: [695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)


## My Solution

```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        nrows, ncolumns = len(grid), len(grid[0])
        visited = set()
        max_area = 0

        def dfs(row, column):
            # Check if the current position is out of bounds
            if row < 0 or row >= nrows or column < 0 or column >= ncolumns:
                return 0
            
            # Check if the current position is water or has been visited
            if grid[row][column] == 0 or (row, column) in visited:
                return 0
            
            visited.add((row, column))  # Mark as visited
            area = 1  # Current tile
            
            # Explore all four directions
            area += dfs(row - 1, column)
            area += dfs(row + 1, column)
            area += dfs(row, column - 1)
            area += dfs(row, column + 1)
            return area

        for i in range(nrows): 
            for j in range(ncolumns):
                if grid[i][j] == 1 and (i, j) not in visited:
                    max_area = max(max_area, dfs(i, j))

        return max_area

```
