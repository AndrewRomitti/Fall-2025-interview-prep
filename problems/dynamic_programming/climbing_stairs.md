# Climbing Stairs

**Link:** (https://neetcode.io/problems/climbing-stairs?list=neetcode150)  
**Difficulty:** Easy  
**Date Solved:** 7/20/25  
**Category:** Dynamic Programming  

## Problem Statement
You are given a number of stairs that you are meant to go up, you can go up one stair or you can go up two stairs at a time, how many possible ways are there to go up the number of stairs you are given  

## Approach
The way that I broke down this DP problem is by first figuring out the recursive brute force solution. This boils down to, you start at 0 and do a recursive call where you go up one stair and a recursive call where you go up 2 stairs, summing those together gets you the total number.  

Now you apply memoization to this brute force solution. I created a hashmap, and before the base case I said if the i (current stair) I am on is in the hashmap, then return that. Else keep going, but now for the sum I want you to add that sum to the hashmap.  

This improves the runtime drastically by not having to go over solutions already seen in the recursive call.  

## Code
```java
class Solution {
	HashMap<Integer, Integer> seen = new HashMap<>();
	public int climbStairs(int n) {
		return climb(0, n);
	}

	private int climb(int i, int n) {
		if (seen.get(i) != null) {
			return seen.get(i);
		}

		if (i == n) {
			return 1;
		}

		if (i > n) {
			return 0;
		}

		seen.put(i, climb(i + 1, n) + climb(i + 2, n));
		return seen.get(i);
	}
``` 

## Time Complexity
**Time Complexity**: O(n)  
**Space Complexity**: O(n)

## Additional Notes
There is a way to do this solution in 5 lines of code, and that is through the bottom-up approach, which is the iterative way to do dynamic programming. The one I did was the top-down approach. For now I am just going to worry about how to make DP solutions, and will revisit iterative approach later.