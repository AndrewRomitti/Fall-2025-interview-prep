# Max Area of Island

**Link:** (https://neetcode.io/problems/max-area-of-island?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 8/20/25  
**Category:** Graphs

## Problem Statement

You are given a grid of integers where 1 represents land and 0 represents water. You must return the maximum area of an island on the grid.

## Approach

This was a very similar problem to the number of islands. Essentially, I just did a BFS to find the islands just like the other problem, but this time I would add to an area every time I explored a new piece of land, and then at the end of the BFS for that particular area I would check to see if this area was bigger than a global counter variable, then return it at the end.

## Code

```java
class Solution {
    private static int[][] directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    int sol = 0;

    public int maxAreaOfIsland(int[][] grid) {
      boolean[][] visit = new boolean[grid.length][grid[0].length];

      for (int r = 0; r < grid.length; ++r) {
        for (int c = 0; c < grid[0].length; ++c) {
          bfs(visit, grid, r, c);
        }
      }

      return sol;
    }

    private void bfs(int[][] grid, boolean[][] visited, int r, int c) {
      Queue<int[]> q = new LinkedList<>();
      visited[r][c] = true;
      q.add(new int[]{r, c});
      int area = 0;

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

          if (rowInRange && colInRange && !visited[newRow][newCol] && grid[newRow][newCol] == 1) {
            visited[newRow][newCol] = true;
            q.add(new int[]{newRow, newCol});
            area++;
          }
        }
      }

      sol = Math.max(sol, area);
    }
}
```

## Time Complexity

**Time Complexity**: O(m _ n)  
**Space Complexity**: O(m _ n)

## Additional Notes

You can also do this solution with dfs as you need to visit all the land either way
