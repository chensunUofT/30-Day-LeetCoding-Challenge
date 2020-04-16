<https://leetcode.com/problems/valid-parenthesis-string/>

If there's no `*` involved, we can just use a `left` variable to count the number of unclosed `(`, add 1 when encountering a `(` and minus 1 when `)`. For the `*`, we can use another variable `star` to count its appearance. When scanning from left to right and there's not enough `(` to match with `)`, one of the `*` (if there is, otherwise the string is invalid) can be consumed as a `(`. After scanning the whole string, if we have more unclosed `(` than `*`, we can also make conclusion that the string is invalid.  
However, if none of the rule is violated as mentioned, it does not necessarily mean that the string is valid, for example, `*(` ends up with `left = 1` and `star = 1 ` , but it's not a valid string because of the order. In order to fix this, we have to scan the string again from right to left with a "mirrored" criteria that a `)` has to come before a `(`. If there's still no violation, we can conclude that the string is valid.

```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        
        left, star = 0, 0
        for char in s:
            if char == '(':
                left += 1
            elif char == ')':
                left -= 1
                if left < 0:
                    if star < 1:
                        return False
                    star -= 1
                    left += 1
            else:
                star += 1
        if left > star:
            return False
        
        right, star = 0, 0
        for char in s[::-1]:
            if char == ')':
                right += 1
            elif char == '(':
                right -= 1
                if right < 0:
                    if star < 1:
                        return False
                    star -= 1
                    right += 1
            else:
                star += 1
        if right > star:
            return False
        
        return True
    
```

The algorithm can be simplified:

- When scanning from left to right, consider all `*` as `(` to see if there're enough `(` to cancel the `)`
- When scanning from right to left, consider all `*` as `)` to see if there're enough `)` to cancel the `(`
- If both conditions are satisfied, the string is valid

```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        
        left = 0
        for char in s:
            if char in ['(', '*']:
                left += 1
            else:
                left -= 1
                if left < 0:
                    return False
                
        right = 0
        for char in s[::-1]:
            if char in [')', '*']:
                right += 1
            else:
                right -= 1
                if right < 0:
                    return False
      
        return True
    
```

There's another great algorithm that I learned from the discussion. We can use two variables `low` and `high` to record the minimal and maximum number of `(` that need to be closed. When encountering a `*`, the `low` would decrease by 1 (`*` could work as a `)` to cancel a `(`) and the `high` would increase by 1 (`*` working as a `(` to be cancelled). When `high` is decreased to less than zero, it means that there's not enough `(` to match with `)` so the string is invalid. Also note that it doesn't make sense if the `low` variable reaches below zero, so we need to reset it to zero in each iteration. After scanning the whole string, we can conclude that the parentheses are perfectly closed if and only if the `low` variable equals zero.

```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        
        low, high = 0, 0
        for char in s:
            if char == '(':
                low, high = low + 1, high + 1
            elif char == ')':
                low, high = low - 1, high - 1
                if high < 0:
                    return False
            else:
                low, high = low - 1, high + 1
            low = max(low, 0)
        return low == 0
            
```

