Here is my solution for the problem: [688. Knight Probability in Chessboard](https://leetcode.com/problems/knight-probability-in-chessboard/)


## My Solution

```python
class Solution:

    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        self.track = {}

        def recursiveKnightProbability(n: int, k: int, row: int, column: int):
            moves = [(1, 2), (2, 1), (-1, 2), (2, -1), (-1, -2), (-2, -1), (1, -2), (-2, 1)] 
            if row < 0 or row >= n or column < 0 or column >= n:
                return 0
            if k == 0:
                return 1
            if (k,row,column) in self.track:
                return self.track[(k,row,column)]
            res = 0
            for i in moves:
                res += recursiveKnightProbability(n, k - 1, row + i[0], column + i[1])/8
            self.track[(k,row,column)] = res
            return res
        return recursiveKnightProbability(n, k, row, column)

```


## Space Optimized Solution

```python
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        moves = [(1, 2), (2, 1), (-1, 2), (2, -1), (-1, -2), (-2, -1), (1, -2), (-2, 1)] 
        dp = [[0 for _ in range(n)] for _ in range(n)]
        dp_prev = [[0 for _ in range(n)] for _ in range(n)]
        dp_prev[row][column] = 1

        for step in range(k):
            for r in range(n):
                for c in range(n):
                    dp[r][c] = 0
                    for dr, dc in moves:
                        prev_r, prev_c = r - dr, c - dc
                        if 0 <= prev_r < n and 0 <= prev_c < n:
                            dp[r][c] += dp_prev[prev_r][prev_c] / 8.0
            dp, dp_prev = dp_prev, dp 

        total_probability = sum(sum(dp_prev[r][c] for c in range(n)) for r in range(n))
        return total_probability
        
```