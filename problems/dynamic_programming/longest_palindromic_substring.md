# Longest Palindromic Substring

**Link:** (https://neetcode.io/problems/longest-palindromic-substring?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 7/25/25  
**Category:** Dynamic Programming  

## Problem Statement
You are given a String and are trying to return the longest palindromic substring from that String.

## Approach
So I wasn't able to solve this problem on my own and it definitely didn't follow the cookie cutter DP structure that I've seen. I was able to figure out a recursive brute force solution after a bit of tinkering, using an isPalindrom function and then building all possible substrings. However, that is extremely inefficient.

The optimized solution makes it so that you go through each character in the string and treat it as the center of the palindrome. You then start expanding left and right only if the characters are equal, meaning it's a valid palindrome. If it is then you check to see if it's longer than the longest palindrome you've tracked and if that's the case then you update the string.

The tricky part is that there are two scenarios, when there is an even and when there is an odd length palindrome. The way to solve this is you first do even where the left and right pointer start at the same place. Then after you do that, you do the odd by having the right pointer start one position to the right of i.

The main pattern I saw here is that I needed to boil it down to what is the sub problem. And that is seeing if a substring is a palindrome in the most efficient way, and that would be by using the center method.


## Code
```java
class Solution {
    public String longestPalindrome(String s) {
        String res = "";
        int resLen = 0;

        for (int i = 0; i < s.length(); ++i) {
            int left = i, right = i;
            while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                if (right - left + 1 > resLen) {
                    res = s.substring(left, right + 1);
                    resLen = right - left + 1;
                }
                left--;
                right++;
            }

            left = i;
            right = i + 1;
            while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                if (right - left + 1 > resLen) {
                    res = s.substring(left, right + 1);
                    resLen = right - left + 1;
                }
                left--;
                right++;
            }
        }

        return res;
    }
}

``` 

## Time Complexity
**Time Complexity**: O(n^2)   
**Space Complexity**: O(1) extra space, O(n) for output string  
