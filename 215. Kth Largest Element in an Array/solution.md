Here is my solution for the problem: [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)


## My Solution

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # Call quickSelect to find the k-th largest element
        # The k-th largest element corresponds to the (len(nums) - k) index in a sorted array
        return self.quickSelect(nums, 0, len(nums) - 1, len(nums) - k)

    def quickSelect(self, nums, low, high, indexToFind):
        # Randomly select a pivot index and swap it with the last element
        r = randint(low, high)
        nums[r], nums[high] = nums[high], nums[r]

        # Set the pivot to the rightmost element after the swap
        p = high  
        i, j = low, high - 1  # Initialize pointers for partitioning
        
        # Partition the array around the pivot
        while i <= j:
            # Move the left pointer to the right while elements are less than the pivot
            if nums[i] < nums[p]: 
                i += 1
            else:
                # Move the right pointer to the left while elements are greater than the pivot
                if nums[j] > nums[p]: 
                    j -= 1
                else:
                    # Swap elements at i and j since they are in the wrong partition
                    nums[i], nums[j] = nums[j], nums[i]
                    i += 1  # Move left pointer to the right
                    j -= 1  # Move right pointer to the left
    
        # Place the pivot in its correct position in the sorted order
        nums[i], nums[p] = nums[p], nums[i]

        # Recursively select the k-th largest element based on the pivot's final position
        if i > indexToFind: 
            # If the pivot index is greater than the index we want, search in the left partition
            return self.quickSelect(nums, low, i - 1, indexToFind)
        elif i < indexToFind: 
            # If the pivot index is less than the index we want, search in the right partition
            return self.quickSelect(nums, i + 1, high, indexToFind)
        else:
            # If the pivot index matches the index we want, return the element at that index
            return nums[indexToFind]
    
```
