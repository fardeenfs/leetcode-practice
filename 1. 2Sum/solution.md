Here is my solution for the problem: [1. Two Sum](https://leetcode.com/problems/two-sum/)


## My Solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        tracked = {}
        for i, num in enumerate(nums):
            if target-num in tracked:
                return [tracked[target-num], i]
            tracked[num] = i
    
```
