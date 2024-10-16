Here is my solution for the problem: [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)


## My Solution

```python
class MyQueue:

    def __init__(self):
        self.stack_one = []
        self.stack_two = []

    def push(self, x: int) -> None:
        self.stack_one.append(x)

    def pop(self) -> int:
        if len(self.stack_two) == 0:
            while self.stack_one:
                self.stack_two.append(self.stack_one.pop())
        return self.stack_two.pop()

    def peek(self) -> int:
        if len(self.stack_two) == 0:
            while self.stack_one:
                self.stack_two.append(self.stack_one.pop())
        return self.stack_two[-1]

    def empty(self) -> bool:
        return not (len(self.stack_one) + len(self.stack_two))
    
```
