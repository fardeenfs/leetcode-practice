Here is my solution for the problem: [430. Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)


## My Solution (Recursive Approach)

```python
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child

def processChild(head):
    current_node = head
    current_node.next = current_node.child
    current_node.next.prev = current_node
    current_node.child = None
    current_node = current_node.next
    while current_node:
        next = current_node.next
        if current_node.child:        
            processed_child, last_node = processChild(current_node)
            current_node = last_node
        current_node.next = next
        if current_node.next:
            current_node.next.prev = current_node
        prev = current_node
        current_node = current_node.next
    return head, prev

class Solution:
    def flatten(self, head: 'Optional[Node]') -> 'Optional[Node]':
        current_node = head
        while current_node:
            next = current_node.next
            if current_node.child:        
                processed_child, last_node = processChild(current_node)
                current_node = last_node
            current_node.next = next
            if current_node.next:
                current_node.next.prev = current_node
            prev = current_node
            current_node = current_node.next
        return head
    
```


# Simplified Solution (Iterative Approach)

```python
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child

class Solution:
    def flatten(self, head: 'Optional[Node]') -> 'Optional[Node]':
        current_node = head
        while current_node:
            if current_node.child:
                tail = current_node.child
                while tail.next:
                    tail = tail.next
                tail.next = current_node.next
                if tail.next != None:
                    tail.next.prev = tail
                current_node.next = current_node.child
                current_node.next.prev = current_node
                current_node.child = None
            else:
                current_node = current_node.next
        return head

```