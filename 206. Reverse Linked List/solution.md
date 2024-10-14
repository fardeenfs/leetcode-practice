Here is my solution for the problem: [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)


## My Solution

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        while head:
            next = head.next # Store the next node for current LL
            head.next = prev # Reverse the next of the current node to the previous node
            prev = head # Update prev to current node
            head = next # Update head to the next node of the LL

        # Since the function breaks when head is none, prev will be the last ListNode (i.e head of the reversed linked list)
        return prev 
    
```
