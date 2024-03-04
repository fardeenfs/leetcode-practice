Here is my solution for the problem: [27. Remove Element](https://leetcode.com/problems/remove-element/)


## My Solution

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        count = nums.count(val)
        end = len(nums) - 1
        for i in range(len(nums) - count):
            if nums[i] == val:
                while nums[end] == val:
                    end -= 1
                nums[i] = nums[end]
                end -= 1
        return len(nums) - count
        
```
