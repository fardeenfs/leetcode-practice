Here is my solution for the problem: [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)


## My Solution

```python
class TrieNode:

    def __init__(self, letter):
        self.letter = letter
        self.next = {}
        self.EOW = False


class Trie:

    def __init__(self):
        self.head = TrieNode('')

    def insert(self, word: str) -> None:
        self.curr = self.head
        for letter in word:
            if letter not in self.curr.next:
                self.curr.next[letter] = TrieNode(letter)
            self.curr = self.curr.next[letter]
        self.curr.EOW = True

    def search(self, word: str) -> bool:
        self.curr = self.head
        for letter in word:
            if letter not in self.curr.next:
                return False
            self.curr = self.curr.next[letter]
        if self.curr.EOW:
            return True
        return False


    def startsWith(self, prefix: str) -> bool:
        self.curr = self.head
        for letter in prefix:
            if letter not in self.curr.next:
                return False
            self.curr = self.curr.next[letter]
        return True
    
```
