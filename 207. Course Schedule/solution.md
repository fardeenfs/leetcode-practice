Here is my solution for the problem: [207. Course Schedule](https://leetcode.com/problems/course-schedule/)


## My Solution

```python
from collections import deque
from typing import List

class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        indegrees = [0] * numCourses
        adj_courses = {i: [] for i in range(numCourses)}

        for prereq, course in prerequisites:
            adj_courses[prereq].append(course)
            indegrees[course] += 1

        # Use deque for efficient popping from the front
        q = deque()
        
        # Initialize the queue with all courses that have no prerequisites
        for i in range(numCourses):
            if indegrees[i] == 0:
                q.append(i)
        
        seen = 0
        
        while q:
            course = q.popleft()
            seen += 1
            
            for neighbor in adj_courses[course]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    q.append(neighbor)

        return seen == numCourses
    
```
