Here is my solution for the problem: [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)


## My Solution (O(N^2) Time Complexity - Brute Force Solution)

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        total = 0
        max_left = height[0]
        max_right = height[len(height)-1]
        for i in range(1, len(height)-1):
            max_left = max(max_left, height[i-1]) # Highest point on the left
            max_right = max(height[i+1:]) # Heighest point on the right
            if min(max_left, max_right) > height[i]:
                # The amount of water above any point is the minimum of the highest points on either side - height of current wall
                total += min(max_left, max_right) - height[i] 
        return total

```


## Optimized Solution Using Two Pointers

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        maxLeft = 0
        maxRight = 0
        total = 0
        while left < right:
            if height[left] <= height[right]: # Selecting the left height if it is smaller or tied (arbitarily chosen) to the right

                # If maxLeft is greater than left height, we know a taller wall exists to the left (maxLeft) and right (due to the above if condition)
                if maxLeft > height[left]: 
                    # We calculate water, since taller walls exist on either side
                    total += maxLeft - height[left]

                # If the current left height is greater than maxLeft, there is no taller wall to the left, so water can't be trapped at the current index.
                else:
                    # We update maxLeft with this higher wall.
                    maxLeft = height[left]

                # We move the left pointer since this is the smaller (or tied) of the left and right according to the first if condition.
                left += 1

            else: # Selecting the right height if it is smaller than the left

                # If maxRight is greater than right height, we know a taller wall exists to the right (maxRight) and left (due to the above if condition)
                if maxRight > height[right]:
                    # We calculate water, since taller walls exist on either side
                    total += maxRight - height[right]

                # If the current right height is greater than maxRight, there is no taller wall to the right, so water can't be trapped at the current index.
                else:
                    # We update maxRight with this higher wall.
                    maxRight = height[right]
                
                # We move the right pointer since this is the smaller of the left and right according to the first if condition.
                right -= 1
                
        return total
        
```

