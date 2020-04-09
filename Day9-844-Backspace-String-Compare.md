<https://leetcode.com/problems/backspace-string-compare/>

It is required to be completed in `O(N)` time and `O(1)` space, so we can't use two stacks/lists to store the string. Instead, we need to traverse the strings backwards from the end of them and compare the two strings character-wise.  
The underlying logic here is that, when the strings are read backwards, if a string starts with a letter, it could not be skipped, so if the letters are different in two strings, just return `False`; if it reads any `#`, we know that the one or multiple following letters would be deleted, so we need to figure out what the index would be after deleting. Here we use a `find_index` helper function with a `delete_count` variable that records how many letters we need to delete/skip.  
The iteration would end if either of the index `i` or `j` is smaller than zero. If they are both negative, which means that the two strings have been completely compared without any difference found, return `True`; otherwise `False`.

```python
class Solution:
    def backspaceCompare(self, S: str, T: str) -> bool:
        
        def find_index(k, string):
            while k >= 0 and string[k] == '#':
                delete_count = 1
                k -= 1
                while delete_count > 0 and k >= 0:
                    if string[k] == '#':
                        delete_count += 1
                    else:
                        delete_count -= 1
                    k -= 1
            return k
                    
        i = find_index(len(S) - 1, S)
        j = find_index(len(T) - 1, T)
        while i >= 0 and j >= 0:
            if S[i] != T[j]:
                return False
            else:
                i = find_index(i-1, S)
                j = find_index(j-1, T)
        return (i < 0 and j < 0)
    
```



