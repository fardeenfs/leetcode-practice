Here is my solution for the problem: [1376. Time Needed to Inform All Employees](https://leetcode.com/problems/time-needed-to-inform-all-employees/)


## My Solution

```python
class Solution:
    def numOfMinutes(self, n: int, headID: int, manager: List[int], informTime: List[int]) -> int:
        adj_dict = {}
        for employee, manager in enumerate(manager):
            if manager in adj_dict.keys():
                adj_dict[manager].append(employee)
            else:
                adj_dict[manager] = [employee]

        q = deque([(headID, 0)])  # (employee, current_time)
        max_time = 0

        while q:
            employee, current_time = q.popleft()
            current_time += informTime[employee]
            max_time = max(max_time, current_time)
            
            if employee in adj_dict:
                for sub in adj_dict[employee]:
                    q.append((sub, current_time))

        return max_time

```
