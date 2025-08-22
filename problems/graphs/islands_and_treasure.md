# Islands and Treasure

**Link:** (https://neetcode.io/problems/islands-and-treasure?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 8/21/25  
**Category:** Graphs

## Problem Statement

You are given a 2D grid full of -1 (water), 0 (treasure), and INF (land). You must find what the distance each piece of land is to the nearest treasure.

## Approach

This problem was a little tricky for me, I knew BFS was what I needed but wasn't sure how to implement it. This problem needed something called a multi-soure BFS. This involves adding multiple nodes to the queue BEFORE starting the BFS (so in this case all the treasure locations), and then you can expand from each of the sources at the same time. So you just do a normal BFS from each treasure chest where you see if it's a piece of land and if it is then you update it to the distance it is from the treasure, and this always ensures it's the nearest distance by the property of BFS.

## Code

```java
class Solution {
    private static int[][] DIRS = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    public void islandsAndTreasure(int[][] grid) {
      Queue<int[]> q = new LinkedList<>();

      for (int r = 0; r < grid.length; ++r) {
        for (int c = 0; c < grid[0].length; ++c) {
          if (grid[r][c] == 0) {
            q.add(new int[]{r, c});
          }
        }
      }

      while (!q.isEmpty()) {
        int[] coord = q.poll();
        for (int[] dir: DIRS) {
          int row = coord[0];
          int col = coord[1];

          int nr = row + dir[0];
          int nc = col + dir[1];

          if (nr >= 0 && nr < grid.length && nc >= 0 && nc < grid[0].length && grid[r][c] == Integer.MAX_VALUE) {
            grid[nr][nc] = grid[row][col] + 1;
            q.add(new int[]{nr, nc});
          }
        }
      }
    }
}
```

## Time Complexity

**Time Complexity**: O(m _ n)  
**Space Complexity**: O(m _ n)

m \* n for initial preprocessing, but also for BFS since you always visit each node exactly once, no repeating.
