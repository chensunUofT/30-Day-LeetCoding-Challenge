<https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/3311/>

This is a very classic *Dynamic Programming* problem. We use a 2-D array `dp[i][j]` to represent the length of longest common subsequence of the `text1[0:i]` and `text2[0:j]`. If the two substrings have the same last character, i.e. `text1[i] == text2[j]`, then `dp[i][j] = dp[i-1][j-1] + 1`; otherwise, since the two substrings don't share the same last letter, the longest common subsequence must be the same with the result of either `text1[i]` and `text2[j-1]`, or `text1[i-1]` and `text2[j]`, in other words, `dp[i][j]` should be the greater value of `dp[i-1][j]` and `dp[i][j-1]`.

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        if not text1 or not text2:
            return 0
        len1, len2 = len(text1), len(text2)
        dp = [[0 for j in range(len2 + 1)] for i in range(len1 + 1)]
        for i in range(1, len1 + 1):
            for j in range(1, len2 + 1):
                if text1[i-1] == text2[j-1]:
                    dp[i][j] = 1 + dp[i-1][j-1]
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        return dp[-1][-1]
        
```



