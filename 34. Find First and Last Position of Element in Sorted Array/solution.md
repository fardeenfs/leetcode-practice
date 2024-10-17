Here is my solution for the problem: [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)


## My Solution

```python
class Solution:
    def binarySearch(self, nums: List[int], target: int, findFirst: bool) -> int:
        low, high = 0, len(nums) - 1
        index = -1
        
        while low <= high:
            mid = low + (high - low) // 2
            
            if nums[mid] < target:
                low = mid + 1
            elif nums[mid] > target:
                high = mid - 1
            else:
                # Target found, update index
                index = mid
                # If finding the first occurrence, continue searching left
                if findFirst:
                    high = mid - 1
                else:
                    # If finding the last occurrence, continue searching right
                    low = mid + 1

        return index

    def searchRange(self, nums: List[int], target: int) -> List[int]:
        first = self.binarySearch(nums, target, True)  # Search for first occurrence
        last = self.binarySearch(nums, target, False)  # Search for last occurrence
        return [first, last]
    
```
