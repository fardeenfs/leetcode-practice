Here is my solution for the problem: [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)


## My Solution

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        index = 1
        root = ListNode(0, next = head) # Blank node to point to the head of the list
        prev = root

        # Iterate the linked list till we reach the left index
        while index < left:          
            prev = head
            head = head.next
            index += 1

        node_before_left_node = prev # Node before the left node to connect after reversal
        start = head # Left node start of reversal

        while index < right + 1:
            current_node = head.next
            head.next = prev
            prev = head
            head = current_node
            index += 1

        # The node that is before the left node is connected to the right node
        node_before_left_node.next = prev 
        
        # The start node is connected to the node after the right node
        start.next = current_node

        return root.next
    
```
