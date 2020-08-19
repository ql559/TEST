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

