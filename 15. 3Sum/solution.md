Here is my solution for the problem: [15. 3Sum](https://leetcode.com/problems/3sum/)


## My Solution (Simple)

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()  # Sort the array to facilitate finding triplets
        output = []

        for i in range(len(nums)-2):  # -2 to leave space for the two other pointers
            # Skip duplicate values for i to ensure uniqueness
            if i > 0 and nums[i] == nums[i-1]:
                continue

            left, right = i + 1, len(nums) - 1
            while left < right:
                total = nums[i] + nums[left] + nums[right]
                if total < 0:
                    left += 1
                elif total > 0:
                    right -= 1
                else:
                    output.append([nums[i], nums[left], nums[right]])
                    # Skip duplicates for left and right pointers
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    left += 1
                    right -= 1

        return output

```
