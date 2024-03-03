Here is my solution for the problem: [720. Longest Word in Dictionary](https://leetcode.com/problems/longest-word-in-dictionary/)


## My Solution

```python
import collections

class Solution:
    def longestWord(self, words: List[str]) -> str:
        words.sort() # For lexicographic sort
        tree = Trie()
        for word in words:
            tree.insertWord(word)

        return tree.longestWordWithBFS()


class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insertWord(self, word):
        node = self.root  # Begin Iteration
        for char in word:
            if char not in node.children: # Need to create a new path
                node.children[char] = TrieNode()
                # Update the history variable to track the word till now
                node.children[char].history = node.history + char 
            node = node.children[char]  # Update for next iteration
        node.completeWord = True  # Denotes that the node denotes the end of a complete word.

    def longestWordWithBFS(self):
        nodes = collections.deque([self.root])
        word = ''
        while len(nodes) > 0:
            node = nodes.popleft() 
            for char, child in node.children.items(): # For each popped node, iterate through its children
                if child.completeWord: # If the node denotes a completed word, add it to nodes to be popped next.
                    nodes.append(child) 
                    # Since we want the max length, update word if the current word is longer
                    if len(child.history) > len(word): 
                        word = child.history 
        return word


class TrieNode:
    def __init__(self):
        self.children = {} # The next characters possible from this node
        self.completeWord = False # If this node denotes and end to a complete word, it will be True
        self.history = '' # Tracks word till this node
    

```
