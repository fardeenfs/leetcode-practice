Here is my solution for the problem: [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)


## My Solution

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        tracked = {}
        longest = 0
        left = 0

        if(len(s) <= 1):
            return len(s)
        
        for right in range(len(s)):
            if s[right] in tracked.keys(): # Check if current char was seen before

                # Check if the previous track is within the current window (i.e. after the left pointer)
                if tracked[s[right]] >= left: 

                    # This is a repeating character so we move the left pointer to after the position this character was first seen
                    left = tracked[s[right]] + 1

            # Update the tracker to store the index
            tracked[s[right]] = right
            longest = max(longest, right - left + 1)

        return longest 
                    
    
```
