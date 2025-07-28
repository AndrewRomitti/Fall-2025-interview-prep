# Maximum Product Subarray

**Link:** (https://neetcode.io/problems/maximum-product-subarray?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 7/27/25  
**Category:** Dynamic Programming  

## Problem Statement
You are given an array of integers, you must return the largest product that can be made from  a subarray within the array.

## Approach (Kadane's Algorithm)
So I did the typical approach of trying to figure out the brute force first, which for dynamic programming problems hasn't been too bad. In this scenario you just keep track of a global max product and then within a double for loop you add to the product making sure it's a valid subarray and then return the global max product after you update it in the loops. This was pretty straight forward, but of course it requires two for loops which is inefficient.

I wasn't able to figure out the optimized solution on my own, which is Kadane's Algorithm. Kadane's Algorithm involves keeping track of the current max and min of the place you are in the sub array. So you loop through the nums and set the max equal to the number times the max, min, or just the number and the min equal to the same thing. Keeping track of the max and min and setting res to the max between res and the global max is a way to solve this problem in just one pass. It's hard to find an overarching pattern here, as it seems this approach seems pretty specific to the problem, but I will think about it more.

## Code
```java
class Solution {
    public int maxProduct(int[] nums) {
        int res = nums[0];

        for (int i = 1; i < nums.length; i++) {
            res = Math.max(res, nums[i]);
        }

        int max = 1;
        int min = 1;

        for (int num: nums) {
            int temp = max * num;
            max = Math.max(Math.max(num * max, num * min), num);
            min = Math.min(Math.min(temp, num * min), num);
            res = Math.max(res, max);
        }

        return res;
    }
}

``` 

## Time Complexity
**Time Complexity**: O(n)   
**Space Complexity**: O(1)  
