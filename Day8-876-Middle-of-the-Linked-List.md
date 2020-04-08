<https://leetcode.com/problems/middle-of-the-linked-list/>

Use `fast` and `slow` pointers to move along the linked list with the speed of two nodes and one node per step. When the `fast` pointer reaches the end of the linked list, the `slow` pointer is approxiamately at the middle depending on whether the length of the linked list is odd or even.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        slow, fast = head, head
        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next
        if fast.next:
            return slow.next
        else:
            return slow
        
```

