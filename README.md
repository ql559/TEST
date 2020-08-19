# Leetcode
## 08/19
409. Longest Palindrome

Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.
Letters are case sensitive, for example, "Aa" is not considered a palindrome here.

class Solution:
    def longestPalindrome(self, s: str) -> int:
        rec = set()
        for c in s:
            if c in rec:
                rec.remove(c)
            else:
                rec.add(c)
        return len(s) - len(rec) + 1 if len(rec) > 0 else len(s)
        
