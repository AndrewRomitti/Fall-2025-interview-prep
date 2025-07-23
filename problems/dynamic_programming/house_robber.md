# House Robber

**Link:** (https://neetcode.io/problems/house-robber?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 7/22/25  
**Category:** Dynamic Programming  

## Problem Statement
You are given an array of houses where the ith index represents how much money is in the house. You are trying to find out how much money you can take from the houses, with the constraint that you can't visit houses that are adjacent to each other.

## Approach (Top down recursive)
I actually really feel like I am getting the gist of top down solutions for dynamic programming. It took me about 15 minutes to solve this problem with memoization and without any hints. I first broke it down into a sub problem. I figured that what you want to know is what is the next best place to go to get the most money. So I kept track of a sum and did a recursive call to check what the maximum is if I added the current house and when to the second next one or if I just went to the next house and didn't add the next house. 

The trickiest part of recursion is the base case, but for all these DP problems they all seem similar. It is when your helper function in the recursion is out of bounds, and then you just simply return 0.  

In my inital approach I thought you could start at any house, so I had a for loop in my main code to check every i for each number, but if you do the right recursive approach this is unnecessary. So essentially, you just do the same DP pattern of breaking down the problem into a sub problem, and in this case it's seeing whether going to the next house and skipping the current one or adding this house and going to the second next one is more profitable and repeating that sub problem for the whole array.  

## Code
```java
class Solution {
    HashMap<Integer, Integer> memo = new HashMap<>();

    public int rob(int[] nums) {
        return solve(nums, 0);
    }

    private int solve(int[] nums, int i) {
        if (memo.containsKey(i)) {
            return memo.get(i);
        }

        if (i >= nums.length) {
            return 0;
        }

        memo.put(i, Math.max(nums[i] +  solve(nums, i + 2), solve(nums, i + 1)));
        return memo.get(i);
    }
}
``` 

## Time Complexity
**Time Complexity**: O(n)  
**Space Complexity**: O(n)

## Additional Notes
There is a way to do this problem in O(1) memory, but that's with the bottom up iterative solution, which is actually pretty straight forward in this problem, but I'll revisit later.
