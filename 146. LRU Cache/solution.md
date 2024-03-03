Here is my solution for the problem: [146. LRU Cache](https://leetcode.com/problems/lru-cache)


## My Solution

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.size = capacity
        self.cache = OrderedDict()  # Initializes the cache using an OrderedDict to maintain the order of insertion.

    def get(self, key):
        if key not in self.cache:
            return -1 
        self.cache.move_to_end(key)  # Moves the accessed key to the end to mark it as recently used.
        return self.cache[key]  # Returns the value associated with the key.

    def put(self, key, val):
        if key in self.cache:
            self.cache.pop(key)  # If the key already exists, remove it first to update its position later.
        self.cache[key] = val  # Inserts or updates the key-value pair in the cache.
        if len(self.cache) > self.size:
            # If the cache exceeds its capacity, remove the least recently used item.
            self.cache.popitem(last=False)  # Removes the first key-value pair (the least recently used item).

```
