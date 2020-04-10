<https://leetcode.com/problems/min-stack/>

The way to keep track of the minimum value of the stack at any time is storing the minimum at that time when pushing each node into the stack.

```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []

    def push(self, x: int) -> None:
        pre_min = self.getMin()
        if pre_min is not None:
            self.stack.append((x, min(x,pre_min)))
        else:
            self.stack.append((x, x))
        
    def pop(self) -> None:
        if self.stack:
            self.stack.pop()

    def top(self) -> int:
        if not self.stack:
            return None
        return self.stack[-1][0]

    def getMin(self) -> int:
        if not self.stack:
            return None
        return self.stack[-1][1]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```



