<https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/3313/>

The first solution is to use a Doubly Linked List to store every unique number by the order of their appearance so that every value could be removed in `O(1)` time, and use a hashmap (dict) to store the pointer to the nodes in the linked list.  
Everytime we want to `add` a number:  

- If the value is not in the hashmap, create a new node with the value, and add it to the end of the linked list.
- If the value is in the hashmap:
  - if it points to an actual node in the linked list, delete that node from the linked list, and point the value to `None` to indicate that the number has appeared before
  - if it points to `None`, this number is not unique so we don't need to do anything

By doing these, each value in the doubly linked list is unique, so we can just return the value of the `head` node to implement `showFirstUnique` .  
(Solution 1)


```python
class FirstUnique:
    
    class DoublyLinkedNode:
        def __init__(self, x):
            self.val = x
            self.prev = None
            self.next = None
    
    def __init__(self, nums: List[int]):
        self.hashmap = {}
        self.head = None
        self.tail = self.head
        for num in nums:
            self.add(num)

    def showFirstUnique(self) -> int:
        if self.head:
            return self.head.val
        else:
            return -1

    def add(self, value: int) -> None:
        if value not in self.hashmap:
            new_node = self.DoublyLinkedNode(value)
            new_node.prev = self.tail
            new_node.next = None
            if not self.tail:
                self.head = new_node
            else:
                self.tail.next = new_node
            self.tail = new_node
            self.hashmap[value] = new_node
        else:
            if self.hashmap[value]:
                node_to_del = self.hashmap[value]
                if node_to_del == self.head:
                    self.head = self.head.next
                if node_to_del == self.tail:
                    self.tail = self.tail.prev
                if node_to_del.next:
                    node_to_del.next.prev = node_to_del.prev
                if node_to_del.prev:
                    node_to_del.prev.next = node_to_del.next
                self.hashmap[value] = None


# Your FirstUnique object will be instantiated and called as such:
# obj = FirstUnique(nums)
# param_1 = obj.showFirstUnique()
# obj.add(value)
```

Another solution uses a queue to store all the values, and use a dict to record number of appearance for each value. To `showFirstUnique`, return the first value in the queue that appeared only once.  
(Solution 2)

```python
from collections import deque

class FirstUnique:

    def __init__(self, nums: List[int]):
        self.q = deque()
        self.d = {}
        for num in nums:
            self.add(num)

    def showFirstUnique(self) -> int:
        while self.q and self.d[self.q[0]] > 1:
            self.q.popleft()
        return self.q[0] if self.q else -1
        
    def add(self, value: int) -> None:
        if value not in self.d:
            self.q.append(value)
            self.d[value] = 1
        else:
            self.d[value] += 1
        

# Your FirstUnique object will be instantiated and called as such:
# obj = FirstUnique(nums)
# param_1 = obj.showFirstUnique()
# obj.add(value)
```

