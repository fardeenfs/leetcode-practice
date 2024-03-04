Here is my solution for the problem: [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)


## My Solution

```python
class Solution:
    def merge(self, intervals):
        intervals = sorted(intervals, key = lambda i: i[0])
        result = [intervals[0]]
        for i in intervals[1:]:
            if i[0] <= result[-1][1]:
                result[-1][1] = max(result[-1][1], i[1])
            else:
                result.append(i)
        return result
```
