Here is my solution for the problem: [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)


## My Solution (Overkil but fun to implement)

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.isEnd = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.isEnd = True

    def getLongestCommonPrefix(self):
        prefix = ""
        node = self.root
        while len(node.children) == 1 and not node.isEnd:
            char, next_node = next(iter(node.children.items()))
            prefix += char
            node = next_node
        return prefix

class Solution:
    def longestCommonPrefix(self, strs):
        if not strs: return ""
        trie = Trie()
        for word in strs:
            trie.addWord(word)
        return trie.getLongestCommonPrefix()

        
```


## Best Solution (Simple)

```python
class Solution:
    def longestCommonPrefix(self, strs) -> str:
        # Initialize the result variable to store the longest common prefix.
        longest_common_prefix = ""
        
        # Sort the list of strings. This makes sure that if there is a common prefix,
        # it will be present in the first and last string due to the alphabetical order.
        strs = sorted(strs)
        
        # Identify the first string and the last string in the sorted list.
        # These two strings represent the minimum and maximum bounds of possible common prefixes.
        first_string = strs[0]
        last_string = strs[-1]
        
        # Iterate over the characters of the first and last string, up to the length of the shorter one.
        for i in range(min(len(first_string), len(last_string))):
            # If the characters at the current index are the same, it's part of the common prefix.
            if first_string[i] == last_string[i]:
                longest_common_prefix += first_string[i]
            else:
                # As soon as a mismatch is found, stop, because the common prefix ends here.
                break
        
        # Return the longest common prefix found.
        return longest_common_prefix

```
