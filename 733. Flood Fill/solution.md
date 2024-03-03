Here is my solution for the problem: [733. Flood Fill](https://leetcode.com/problems/flood-fill/)


## My Solution

```python
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        # Get the original color of the starting pixel
        originalColor = image[sr][sc]
        
        # If the new color is the same as the original color, no action is required
        if originalColor == newColor:
            return image
        
        # Call the helper function to apply the flood fill
        self.floodFillHelper(image, sr, sc, originalColor, newColor)
        return image

    def floodFillHelper(self, image, sr, sc, originalColor, newColor):
        # Base case: Check if the current pixel is out of bounds or not the original color
        if sr < 0 or sr >= len(image) or sc < 0 or sc >= len(image[0]) or image[sr][sc] != originalColor:
            return
        
        # Change the color of the current pixel to the new color
        image[sr][sc] = newColor
        
        # Recursively apply flood fill to the four adjacent pixels
        self.floodFillHelper(image, sr-1, sc, originalColor, newColor)  # Up
        self.floodFillHelper(image, sr+1, sc, originalColor, newColor)  # Down
        self.floodFillHelper(image, sr, sc-1, originalColor, newColor)  # Left
        self.floodFillHelper(image, sr, sc+1, originalColor, newColor)  # Right


```
