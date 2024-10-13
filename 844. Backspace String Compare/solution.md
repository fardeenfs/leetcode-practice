Here is my solution for the problem: [844. Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)


## My Solution (Simple Stack Approach) - Space Complexity O(a+b)

```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        def cleanedString(word):
            stack = []
            for letter in word:
                if letter!="#":
                    stack.append(letter)
                else:
                    if len(stack) > 0:
                        stack.pop()
            return "".join(stack)

        s = cleanedString(s)
        t = cleanedString(t)
        if s == t:
            return True
        return False
    
```


## Optimized Solution (Two Pointer Solution) - Space Complexity O(1)

```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        a, b = len(s) - 1, len(t) - 1

        def resolve(i, x):
            while i >= 0 and x[i] == "#":
                remove = 1
                i -= 1
                while i >= 0 and remove > 0:
                    if x[i] == "#":
                        remove += 1
                    else:
                        remove -= 1
                    i -= 1
            return i

        while a >= 0 or b >= 0:
            # Resolve the current effective index for both strings (backspace with #)
            a = resolve(a, s)
            b = resolve(b, t)

            if a < 0 or b < 0: # Check if either string have completed processing
                # return True if both strings have completed processing (i.e. True and True)
                # return False if only one has completed processing.
                return a < 0 and b < 0 

            if s[a] != t[b]: #
                return False
            a -= 1
            b -= 1
        return True
    
```
