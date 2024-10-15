Here is my solution for the problem: [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)


## My Initial Solution - Space Complexity O(n)

```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        nodes = set()
        while head:
            if head in nodes:
                return head
            nodes.add(head)
            head = head.next
        return None
    
```


## My Optimal Solution - Space Complexity O(1) - Floyd's Tortoise and Hare Algorithm 

```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        tortoise = head # Slow Pointer
        hare = head # Fast Pointer
        while tortoise and hare:
            tortoise = tortoise.next
            if hare.next == None:
                return None
            hare = hare.next.next
            if tortoise == hare: # If the pointers meet, a cycle exists. We attempt to find the start of the cycle
                p1 = head # Start of the linked list
                p2 = hare # Node where the slow and fast pointers met
                while p1 != p2: # Iterate until the next iteration from the start and meeting point meet which denote the start of the cyle
                    p1 = p1.next
                    p2 = p2.next
                return p1 
        return None
    
```
