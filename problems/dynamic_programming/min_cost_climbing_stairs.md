# Min Cost Climbing Stairs

**Link:** (https://neetcode.io/problems/min-cost-climbing-stairs)  
**Difficulty:** Easy  
**Date Solved:** 7/21/25  
**Category:** Dynamic Programming  

## Problem Statement
You are given an array of costs, which represent how much each stair costs to go up. You are able to go up one or two stairs, and you are able to start at the 0th index stair or the 1st index stair. You need to find the minimum cost to go up the staircase.

## Approach (Top down recursive)
So this is very similar to the original climbing stairs problem, but instead of finding distinct ways for something you are finding the minimum cost. As with the previous problem the first thing I did was figure out the recursive brute force solution.   

This boils down to creating a helper function that finds what the minimum cost to reach the top of the staircase is at the ith index. The hardest part of creating these recursive functions is the base case. The base case in this scenario is whenever the i you are at is greater than the length of the cost array, because that means you have reached the top of the staircase.  

Now once you have this helper method, in the main method you run the method on the first stair and the second stair and return the minimum. Then to optimize this you apply memoization in essentially the exact same way as the original stairs problem. You create a hashmap that adds the current index you're at in the helper method, and the minimum cost to make it to the top from that index. Then before the base case if the i you are it is in the hashmap, then you return that value.

In this scenario since you know how big the hashmap is, you could also use an array, which would improve memory.

## Code
```java
class Solution {
    HashMap<Integer, Integer> seen = new HashMap<>();
    
    public int minCostClimbingStairs(int[] cost) {
        return Math.min(solve(cost, 0), solve(cost, 1));
    }

    private int solve(int[] cost, int i) {
        if (seen.containsKey(i)) {
            return seen.get(i);
        }

        if (i >= cost.length) {
            return 0;
        }

        seen.put(i, cost[i] + Math.min(solve(cost, i + 1), solve(cost, i + 2)));

        return seen.get(i);
    }
}
``` 

## Time Complexity
**Time Complexity**: O(n)  
**Space Complexity**: O(n)

## Additional Notes
There is a way to do this problem in O(1) memory by just keeping track of the first next step and the second next step, but for now I am just practicing DP so I am just trying to understand that.