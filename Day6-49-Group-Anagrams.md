<https://leetcode.com/problems/group-anagrams/>

We hope to use a dict/Hashmap data stucture where the keys are the "count/combination" of letters for each word and the values are the grouped anagrams. Note that none of *set*, *Counter* or *list* is hashable, I come up with the idea of using an vector (actually a tuple in this problem) to represent the letter apperance in each word.

```python
from collections import Counter

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        
        def word_to_vec(word):
            vec = [0] * 26
            ct = Counter(word)
            for letter in ct:
                vec[ord(letter) - ord('a')] = ct[letter]
            return tuple(vec)
        
        res_dict = {}
        for word in strs:
            vec = word_to_vec(word)
            if vec not in res_dict:
                res_dict[vec] = [word]
            else:
                res_dict[vec].append(word)
        return res_dict.values()
    
```

