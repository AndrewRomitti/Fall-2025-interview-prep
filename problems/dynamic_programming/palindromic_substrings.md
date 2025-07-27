# Longest Palindromic Substring

**Link:** (https://neetcode.io/problems/palindromic-substrings?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 7/26/25  
**Category:** Dynamic Programming  

## Problem Statement
You are given a String and are trying to return the number of palindromic substrings in that array.

## Approach
After doing the longest palindromic substring you literally do the same approach but even simpler. You use the optimization where you loop through each character and treat it like the center and expand left and right if the characters are the same and each time you do that you increment the count. Then you check the even ones by having left start at i and right start at i + 1 instead of both starting at i and do the same exact thing. I now know the trick to find all palindromic substrings with two pointers so getting the optimized solution with this problem was really straight forward.


## Code
```java
class Solution {
    public int countSubstrings(String s) {
        int count = 0;
        for (int i = 0; i < s.length(); ++i) {
            int l = i;
            int r = i;
            while (l >= 0 && r < s.length() && s.charAt(l) == s.charAt(r)) {
                count++;
                l--;
                r++;
            }
            
            l = i;
            r = i + 1;
            while (l >= 0 && r < s.length() && s.charAt(l) == s.charAt(r)) {
                count++;
                l--;
                r++;
            }
        }

        return count;
    }
}


``` 

## Time Complexity
**Time Complexity**: O(n^2)   
**Space Complexity**: O(1)
