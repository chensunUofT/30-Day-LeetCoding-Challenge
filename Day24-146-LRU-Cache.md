<https://leetcode.com/problems/lru-cache/>

The [OrderedDict](https://docs.python.org/3.8/library/collections.html#collections.OrderedDict) data structure in Python3 is perfect for this problem. When we `get` the value of an existing key for the dictionary, we need to move the key to the end; when we `put` a new key-value pair, it also needs to be appended to the end of the dictionary, and the item at the first item has to be popped if the maximum capacity is exceeded.   

```python
from collections import OrderedDict

class LRUCache:

    def __init__(self, capacity: int):
        self.od = OrderedDict()
        self.max_cap = capacity

    def get(self, key: int) -> int:
        if key in self.od:
            self.od.move_to_end(key)
            return self.od[key]
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if key in self.od:
            self.od.move_to_end(key)
            self.od[key] = value
        else:
            if len(self.od) == self.max_cap:
                self.od.popitem(last=False)
            self.od[key] = value
            self.od.move_to_end(key)


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

