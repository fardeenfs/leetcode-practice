Here is my solution for the problem: [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/)


## My Solution

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        def isPalindrome(s: str) -> bool:
            left = 0
            right = len(s) - 1
            while right > left:
                if s[left] != s[right]:
                    return False
                left += 1
                right -= 1
            return True
        left = 0
        right = len(s) - 1
        while right > left:
            if s[left] != s[right]:
                return isPalindrome(s[:left]+s[left+1:]) or isPalindrome(s[:right]+s[right+1:])
            left += 1
            right -= 1
        return True
    
```


## Fun Solution (Same logic but fewer lines)

```python
class Solution:
    def validPalindrome(self, s: str, strict = False) -> bool:
        left = 0
        right = len(s) - 1
        while right > left:
            if s[left] != s[right]:
                if (strict):
                    return False
                else:
                    return self.validPalindrome(s[:left]+s[left+1:], True) or self.validPalindrome(s[:right]+s[right+1:], True)
            left += 1
            right -= 1
        return True

```