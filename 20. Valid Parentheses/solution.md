Here is my solution for the problem: [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)


## My Solution

```python
class Solution:
    def isValid(self, s: str) -> bool:
        closing = {
            ")": "(",
            "]": "[",
            "}": "{"
        }
        stack = []
        for char in s:
            if char in closing.values():
                stack.append(char)
            elif char in closing.keys():
                if len(stack) == 0:
                    return False
                elif stack[-1] == closing[char]:
                    stack.pop()
                else:
                    return False
        if len(stack) == 0:
            return True
        return False

```
