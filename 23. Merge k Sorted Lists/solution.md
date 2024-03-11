Here is my solution for the problem: [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)


# Best Runtime Using Priority Queues

```python
import heapq

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        dummy = ListNode(None)
        current = dummy

        # Prepare the heap, initially contains the first node of each list (if not empty)
        heap = [(node.val, i, node) for i, node in enumerate(lists) if node]
        heapq.heapify(heap)

        # Continue until the heap is empty
        while heap:
            _, i, node = heapq.heappop(heap)
            current.next = node
            current = current.next

            # If the popped list has more nodes, add the next node to the heap
            if node.next:
                heapq.heappush(heap, (node.next.val, i, node.next))

        return dummy.next

```


# Alternate Solution With Constant Memory

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        head = cur_node = ListNode(0)  # Dummy node to simplify head handling
        cont = set()  # Tracks exhausted lists

        while len(cont) < len(lists):
            min_val, node = float('inf'), None  # Use float('inf') for comparison
            for index, ln in enumerate(lists):
                if ln and ln.val < min_val:
                    min_val, node = ln.val, index
                elif ln is None:
                    cont.add(index)

            if node is not None:
                if cur_node:  # Attach new node to the result list
                    cur_node.next = lists[node]
                    cur_node = cur_node.next
                lists[node] = lists[node].next
                if lists[node] is None:  # Mark list as exhausted if needed
                    cont.add(node)
            else:
                break  # No more nodes to process

        return head.next  # Skip dummy node

```