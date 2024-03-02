Here is my solution for the problem: [234. Minimum Time Difference](https://leetcode.com/problems/minimum-time-difference/)


## Simple Solution using O(n) space and O(n) time

```python
class Solution:
    def findMinDifference(self, timePoints: List[str]) -> int:
        for i in range(len(timePoints)):
            hours = int(timePoints[i][:2])
            minutes = int(timePoints[i][3:])
            timePoints[i] = 60 * hours + minutes # Convert time to minutes

        timePoints = sorted(timePoints) # Sort the time points
        prev = timePoints[0]
        answer = 1440 # Maximum difference possible in a day

        for i in range(1, len(timePoints)):
            if timePoints[i] == prev:
                return 0
            
            if timePoints[i] - prev < answer:
                answer = timePoints[i] - prev 
            prev = timePoints[i]
        
        if (1440 - timePoints[-1] + timePoints[0] < answer):
            answer = 1440 - timePoints[-1] + timePoints[0] # Check the difference between the first and last time points for circular time (next day)

        return answer
```

## Get rid of the last if statement

```python
class Solution:
    def findMinDifference(self, timePoints: List[str]) -> int:
        for i in range(len(timePoints)):
            hours = int(timePoints[i][:2])
            minutes = int(timePoints[i][3:])
            timePoints[i] = 60 * hours + minutes # Convert time to minutes

        timePoints = sorted(timePoints) # Sort the time points
        prev = timePoints[0]

        # We can initialize the answer with the difference between the first and last time points for circular time (next day)
        answer = answer = 1440 - timePoints[-1] + timePoints[0] 

        for i in range(1, len(timePoints)):
            if timePoints[i] == prev:
                return 0
            
            if timePoints[i] - prev < answer:
                answer = timePoints[i] - prev 
            prev = timePoints[i]

        return answer
```