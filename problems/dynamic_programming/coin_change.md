# Coin Change

**Link:** (https://neetcode.io/problems/coin-change?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 7/24/25  
**Category:** Dynamic Programming  

## Problem Statement
You are given an array of coin denominations and an amount, you must find the minimum number of coins it takes to make the amount.

## Approach (Bottom-up recursive)
My approach for all these DP problems has been the same so far. Figure out what the recursive solution is (that's the easiest for me to understand) and then implement the top down solution, and afterwards try and understand the bottom up. The bottom up is usually always more straight forward, but that's just where my mind goes.  

For this problem I needed some hints, I figured out the main idea of the recursion, but the edge case of when the amount couldn't be made tripped me up.  

Anyways, the main way to solve this problem is that you use backtracking, so you either pick a coin denomination or you don't and then you try each option for all of the possible coins. Where each amount path you've gone down you store in an array for memoization.  

For the bottom up approach, you start at 0 (which it seems you do for all bottom up approaches), and you try go up each amount. You make your memoization array full of numbers bigger than the amount, and essentially do 1 + arr[currAmount - coin] and if it exists then you set that to your current index. You repeat that until you reach the amount very straight forward.

## Code
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] memo = new int[amount + 1];
        Arrays.fill(memo, amount + 1);
        memo[0] = 0;

        for (int a = 1; a <= amount; a++) {
            for (int coin: coins) {
                if (a - coin >= 0) {
                    memo[a] = Math.min(memo[a], 1 + memo[a - coin]);
                }
            }
        }

        if (memo[amount] <= amount && memo[amount] >= 0) {
            return memo[amount];
        } else {
            return -1;
        }
    }
}
``` 

## Time Complexity
**Time Complexity**: O(t*n)   
**Space Complexity**: O(t)  
where t is amount and n is coins
