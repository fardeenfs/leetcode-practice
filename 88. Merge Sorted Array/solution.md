Here is my solution for the problem: [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)


## My Solution

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        index1 = m - 1
        index2 = n - 1
        total = m + n - 1

        while index2 >= 0:
            if index1 < 0 or nums2[index2] > nums1[index1]:
                nums1[total] = nums2[index2]
                index2 -= 1
            else:
                nums1[total] = nums1[index1]
                index1 -= 1
            total -= 1

```
