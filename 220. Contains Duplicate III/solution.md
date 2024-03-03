Here is my solution for the problem: [220. Contains Duplicate III](https://leetcode.com/problems/contains-duplicate-iii/)


# Intuition
- Think of buckets as containers that group numbers together based on their value. Each bucket can hold numbers within a certain range. The size of this range is determined by valueDiff, the maximum allowed difference between any two numbers.
- The size of each bucket is set to valueDiff + 1. This ensures that if two numbers are in the same bucket, their difference is guaranteed to be less than or equal to valueDiff. For example, if valueDiff is 3, then bucket size is 4, meaning any two numbers in the same bucket will have a difference of 0 to 3.
- The bucket key is calculated by dividing the number (num) by the bucket size. This calculation ensures that numbers are placed into buckets based on their value range. For instance, with a valueDiff of 3 (bucket size of 4), numbers 0 to 3 go into one bucket, 4 to 7 into another, and so on.

# Approach
- If two numbers fall into the same bucket, they automatically satisfy the valueDiff condition. We only need to ensure that they also meet the indexDiff condition.
- To account for cases where two numbers are close in value but span two buckets, we also check numbers in the bucket immediately before and after the current number's bucket. This is because a number at the high end of one bucket and a number at the low end of the adjacent bucket could be within valueDiff of each other.
- To maintain the indexDiff condition, the algorithm only considers the last indexDiff + 1 numbers at any point in time. This is achieved by adding the current number to its respective bucket and removing the number that is indexDiff positions back from its bucket as we iterate through the array.

# Complexity
- Time complexity:
$$O(n)$$

- Space complexity:
$$O(min(n,k))$$
n is the total number of elements in the nums array.
k is the indexDiff, which limits the number of elements (and thus buckets) considered at any point.

# My Solution
```
class Solution:
    def containsNearbyAlmostDuplicate(self, nums, indexDiff, valueDiff):
        # Initialize buckets
        buckets = {}
        bucketSize = valueDiff + 1
        
        for i, num in enumerate(nums):
            bucketKey = num // bucketSize
            
            # Check if the bucket already contains a nearby almost duplicate
            if bucketKey in buckets:
                return True
            
            # Check the adjacent buckets
            if bucketKey - 1 in buckets and abs(num - buckets[bucketKey - 1]) < bucketSize:
                return True
            if bucketKey + 1 in buckets and abs(num - buckets[bucketKey + 1]) < bucketSize:
                return True
            
            # Add the current number to its bucket
            buckets[bucketKey] = num
            
            # Remove the element whose index difference is more than indexDiff
            if i >= indexDiff:
                del buckets[nums[i - indexDiff] // bucketSize]
        
        return False

```