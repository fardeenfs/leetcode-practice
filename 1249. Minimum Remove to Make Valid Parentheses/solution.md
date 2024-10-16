Here is my solution for the problem: [1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)


## My Solution

```python
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        stack = []
        indices = []
        s = list(s)
        for i, char in enumerate(s):
            if char == "(":
                stack.append("(")
                indices.append(i)
            elif char == ")":
                if len(stack) == 0:
                    stack.append(")")
                    indices.append(i)
                elif stack[-1] == "(":
                    stack.pop()
                    indices.pop()
                else:
                    stack.append(")")
                    indices.append(i)

        for i in indices:
            s[i] = ''
            
        return ''.join(s)
            
```
