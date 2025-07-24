# House Robber II

**Link:** (https://neetcode.io/problems/house-robber-ii?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 7/23/25  
**Category:** Dynamic Programming  

## Problem Statement
You are given an array of houses where the ith index represents how much money is in the house. You are trying to find out how much money you can take from the houses, with the constraint that you can't visit houses that are adjacent to each other AND **the houses are in a circle so the first and last house are considered adjacent to each other** (new part for this problem)

## Approach (Top down recursive)
So I did need some hints to figure this out. I had the general idea that there needed to be a way to know if the first element was included in the base case, and if it was then just skip the last element. However, the actual way to do this is much more clever and straightforward. You just make two arrays, one that includes the first element and excludes the last, and another array that is the opposite and you just run normal house robber on the two arrays and take the max. This makes intuitive sense because you either have the last or the first house included in your solution not both.  

Additionally, I looked into how to do the space optimized solution for house robber and it's really straight forward. Because you just need to keep track of the sum and the house that is two away, then you can just do a two pointer approach. You have two pointers that both start at 0 and you loop over the numbers, making one pointer the current running maximum and then making the other pointer point to the next house to go to. You can imagine rob1 as robbing the current house and skipping the previous one, and you can imagine rob2 as skipping the current house and taking the loot from the previous house. The main thing is that these two pointers keep track of **previous houses**.

## Code
```java
class Solution {
    public int rob(int[] nums) {
        int[] first = Arrays.copyOfRange(nums, 0, nums.length - 1);
        int[] second = Arrays.copyOfRange(nums, 1, nums.length);

        return Math.max(nums[0], Math.max(solve(first), solve(second)));
    }

    private int solve(int[] nums) {
        int rob1 = 0, rob2 = 0;

        for (int num: nums) {
            int newRob = Math.max(num + rob1, rob2);
            rob1 = rob2;
            rob2 = newRob;
        }

        return rob2;
    }
}
``` 

## Time Complexity
**Time Complexity**: O(n)  
**Space Complexity**: O(1)
