# Rotting Fruit

**Link:** (https://neetcode.io/problems/rotting-fruit?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 8/23/25  
**Category:** Graphs

## Problem Statement

You are given a grid where 0 represents an empty cell, 1 represents fresh fruit, and 2 represents rotten fruit. Every minute if a fresh fruit is horizontally or vertically next to a rotten fruit, then that fresh fruit becomes rotten. You must find how long it will take for all fruit to become rotten, if it's impossible return -1

## Approach

This problem was pretty straight forward. You do a multi-source BFS on each rotten fruit, and at each level of the BFS you increment minutes, if a piece of fresh fruit still remains after the queue is empty, you know to return -1.

The tricky part of this problem was keeping track of the minutes. To do this you had to keep track of the size of the queue each iteration. Only rotten fruit were put in the queue, so that's how many rotten fruit were spreading this wave. You only add a minute for each wave of spreading.

## Code

```java
class Solution {
    private static int[][] DIRS = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    int minutes = 0;
    int fresh = 0;

    public int orangesRotting(int[][] grid) {
      Queue<int[]> q = new LinkedList<>();

      for (int r = 0; r < grid.length; r++) {
        for (int c = 0; c < grid[0].length; c++) {
          if (grid[r][c] == 1) {
            fresh++;
          }
          if (grid[r][c] == 2) {
            q.add(new int[]{r, c});
          }
        }
      }

      bfs(grid, q);

      return fresh == 0 ? minutes : -1;
    }

    private void bfs(int[][] grid, Queue<int[]> q) {
      while(fresh > 0 && !q.isEmpty()) {
        int size = q.size();

        for (int i = 0; i < size; ++i) {
            int[] coord = q.poll();
            int row = coord[0];
            int col = coord[1];

          for (int[] dir: DIRS) {
            int dr = dir[0];
            int dc = dir[1];

            int nr = row + dr;
            int nc = col + dc;

            if (nr >= 0 && nr < grid.length && nc >= 0 && nc < grid[0].length
            && grid[nr][nc] == 1) {
              grid[nr][nc] = 2;
              q.add(new int[]{nr, nc});
              fresh--;
            }
          }
        }

        minutes++;
      }
    }
}
```

## Time Complexity

**Time Complexity**: O(m _ n)  
**Space Complexity**: O(m _ n)
