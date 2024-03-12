Here is my solution for the problem: [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)


## My Solution

```python
class Solution(object):
    def strStr(self, haystack, needle):
        for i in range(len(haystack) - len(needle) + 1):
            if haystack[i : i+len(needle)] == needle:
                return i      
        return -1
        
```


## With Built-in Function

```python
class Solution(object):
    def strStr(self, haystack, needle):
        return haystack.find(needle)
        
```
