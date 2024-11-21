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
        curr = self.head
        for letter in word:
            if letter not in curr.next:
                curr.next[letter] = TrieNode(letter)
            curr = curr.next[letter]
        curr.EOW = True

    def search(self, word: str) -> bool:
        curr = self.head
        for letter in word:
            if letter not in curr.next:
                return False
            curr = curr.next[letter]
        if curr.EOW:
            return True
        return False


    def startsWith(self, prefix: str) -> bool:
        curr = self.head
        for letter in prefix:
            if letter not in curr.next:
                return False
            curr = curr.next[letter]
        return True


```
