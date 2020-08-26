# Leetcode
## 08/19
### 409. Longest Palindrome [E]
```
Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.
Letters are case sensitive, for example, "Aa" is not considered a palindrome here.
```
class Solution:
    def longestPalindrome(self, s: str) -> int:
        rec = set()
        for c in s:
            if c in rec:
                rec.remove(c)
            else:
                rec.add(c)
        return len(s) - len(rec) + 1 if len(rec) > 0 else len(s)
        
### 5. Longest Palindromic Substring [M]
```
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ''
        # odd like 'aba'
        for i in range(len(s)):
            temp = self.helper(s, i, i)
            if len(temp) > len(res):
                res = temp
        # even like 'abba'
        for i in range(len(s)):
            temp = self.helper(s, i, i + 1)
            if len(temp) > len(res):
                res = temp
        return res
    
    def helper(self, arr, l, r):
        while l >= 0 and r < len(arr) and arr[l] == arr[r]:
            l -= 1
            r += 1
        return arr[l + 1 : r]

### 1143. Longest Common Subsequence [M]
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
    DP SOLUTION:
        m = len(text1)
        n = len(text2)
        dp = [[0] * (n + 1) for _ in range(m + 1)]
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if text1[i - 1] == text2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                else:
                    dp[i][j] = max(dp[i][j - 1], dp[i - 1][j])
        return dp[m][n]
        
    Recursion SOLUTION: TLE
        return self.helper(text1, text2, 0, 0)
     def helper(self, s1, s2, i, j):
        if i == len(s1) or j == len(s2):
            return 0
        if s1[i] == s2[j]:
            return self.helper(s1, s2, i + 1, j + 1) + 1
        else:
            return max(self.helper(s1, s2, i + 1, j), self.helper(s1, s2, i, j + 1))
            
## 08/24 Citadel OA (in OA word file)            

## 08/25
### 20. Valid Parentheses [E]
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        dic = {']':'[', ')':'(', '}':'{'}
        for char in s:
            if char in dic.values():
                stack.append(char)
            elif char in dic:
                if not stack or stack.pop() != dic[char]:
                    return False
            else:
                return False
        return len(stack) == 0
        
### 32. Longest Valid Parentheses [H]  Akuna Capital 面经
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        stack = [0]
        res = 0
        for c in s:
            if c == '(':
                stack.append(0)
            else:
                if len(stack) > 1:
                    val = stack.pop()
                    stack[-1] += val + 2
                    res = max(res, stack[-1])
                else:
                    stack = [0]
        return res


### 
