Here is my solution for the problem: [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)


## My Solution

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        table = []
        if len(cost) < 2:
            return 0
        table.append(cost[0])
        table.append(cost[1])
        for i in cost[2::]:
            table.append(i+min(table[-1],table[-2]))
        return min(table[-1],table[-2])

```