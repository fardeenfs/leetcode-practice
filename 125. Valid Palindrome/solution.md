Here is my solution for the problem: [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)


## My Solution

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = re.sub(r'[^A-Za-z0-9]',"", s).lower()
        left = 0
        right = len(s) - 1
        while right > left:
            if s[left] != s[right]:
                return False
            left += 1
            right -= 1
        return True
    
```
