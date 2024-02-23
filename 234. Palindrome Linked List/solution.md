Here is my solution for the problem: [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)


## Simple Solution using O(n) space and O(n) time

code_snippets
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        values = []
        values.append(str(head.val))
        while head.next != None:
            head = head.next
            values.append(str(head.val))
        if (values == values[::-1]):
            return True
        return False
```


## O(n) time and O(1) space - Optimal Solution

code_snippets
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        fast = slow = head

        # fast pointer moves twice as fast as the slow pointer, so when fast gets to the end, slow will be in the middle.
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next

        prev = None
        while slow:
            tmp = slow.next
            slow.next = prev
            prev = slow
            slow = tmp

        # Check Palindrome
        left, right = head, prev

        while right: 
            if left.val != right.val:
                return False
            left = left.next
            right = right.next
        return True
```

