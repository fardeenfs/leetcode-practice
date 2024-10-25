Here is my solution for the problem: [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)


# Approach
Iterate through the grid. When you find a 1 that is not tracked (belongs to another island chain), increment the island count. Start a BFS from this point to find all its connection and add it to tracked, so that they are not recounted. 


# My Solution (On October 25th 2024)

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        all_directions = [(-1,0), (1,0), (0,1), (0, -1)]
        islands = 0

        def traverse(grid, row, column):
            if row < 0 or row > len(grid) - 1 or column < 0 or column > len(grid[0]) - 1:
                return
            if grid[row][column] == "1":
                grid[row][column] = "0"
                for direction in all_directions:
                    traverse(grid, row + direction[0], column + direction[1])
                
        for row_no, row in enumerate(grid):
            for column_no, column in enumerate(row):
                if grid[row_no][column_no] == "1":
                    traverse(grid, row_no, column_no)
                    islands += 1
        return islands

```


# My Solution (On March 3rd 2024)

```python
class Solution:
    def checkConnections(self, grid, row, column, checked):
        nrows = len(grid)
        ncolumns = len(grid[0])
        track = {}
        if row > 0:
            track[(row-1, column)] = grid[row-1][column]
        if row < nrows - 1:
            track[(row+1, column)] = grid[row+1][column]
        if column > 0:
            track[(row, column-1)] = grid[row][column-1]
        if column < ncolumns - 1:
            track[(row, column+1)] = grid[row][column+1]
        
        response = []
        for key, value in track.items():
            if value == '1' and key not in checked:
                response.append(key)
        return response

    def numIslands(self, grid):
        tracked = {}
        island_count = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                # First 1 of an island chain
                if grid[i][j] == '1' and (i, j) not in tracked:
                    island_count += 1
                    # BFS approach to find all the points attached to the chain and track them, so that
                    # that they are not counted as a separate island
                    connections = {(i, j)}
                    while connections: 
                        item = connections.pop()
                        if item not in tracked:
                            tracked[item] = True
                            connections.update(self.checkConnections(grid, item[0], item[1], tracked))
        return island_count

```
