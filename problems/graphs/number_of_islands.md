# Number of Islands

**Link:** (https://neetcode.io/problems/count-number-of-islands?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 8/19/25  
**Category:** Graphs

## Problem Statement

You are given a grid of characters where '1' represents land and '0' represents water. You must count and return the number of islands on the grid

## Approach

This is my first time jumping into a graph problem, so I had to watch a video to get the gist of DFS and BFS and how to code it. For this problem, I implemented the BFS approach. This involved creating a visited set and then looping through each row and column in the grid and if it was land and not in the visited set, you did BFS on that coordinate and added 1 to the number of islands. Then BFS would search for all the land around it and visit that and add it to the visited set.

## Code

```java
class Solution {
    private static int[][] directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    public int numIslands(char[][] grid) {
      int ROWS = grid.length, COLS = grid[0].length;
      boolean[][] visit = new boolean[ROWS][COLS];
      int islands = 0;

      for (int r = 0; r < ROWS; r++) {
        for (int c = 0; c < COLS; c++) {
          if (grid[r][c] == '1' && !visit[r][c]) {
            bfs(grid, visit, r, c);
            islands++;
          }
        }
      }

      return islands;
    }

    private void bfs(char[][] grid, boolean[][] visited, int r, int c) {
      Queue<int[]> q = new LinkedList<>();
      visited[r][c] = true;
      q.add(new int[]{r, c});

      while(!q.isEmpty()) {
        int[] coord = q.poll();
        int row = coord[0];
        int col = coord[1];

        for (int[] dir: directions) {
          int dr = dir[0];
          int dc = dir[1];

          int newRow = row + dr;
          int newCol = col + dc;

          boolean rowInRange = newRow >= 0 && newRow < grid.length;
          boolean colInRange = newCol >= 0 && newCol < grid[0].length;

          if (rowInRange && colInRange && !visited[newRow][newCol] && grid[newRow][newCol] == '1') {
            visited[newRow][newCol] = true;
            q.add(new int[]{newRow, newCol});
          }
        }
      }
    }
}
```

## Time Complexity

**Time Complexity**: O(m _ n)  
**Space Complexity**: O(m _ n)

## Additional Notes

You can also do this solution with dfs as you need to visit all the land either way
