<https://leetcode.com/problems/last-stone-weight/>

Use a heap to store the opposite values of all the orginal elements so that we can use `pop` operation to get the maximum value instead of the minimum.

```python
class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        heap = [-s for s in stones]
        heapq.heapify(heap)
        while len(heap) > 1:
            y = - heapq.heappop(heap)
            x = - heapq.heappop(heap)
            if y > x:
                heapq.heappush(heap, x-y)
        if heap:
            return -heap[0]
        else:
            return 0
        
```

