# Pacific Atlantic Water Flow

**Link:** (https://neetcode.io/problems/pacific-atlantic-water-flow?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 8/24/25  
**Category:** Graphs

## Problem Statement

You are a given a grid of heights that represent different sea levels. The top and left borders represent the pacific ocean, the bottom and right borders represent the atlantic ocean.

You must return the coordinates of which heights can reach both the pacific and atlantic ocean. Heights that are equal to or less than others can flow into that coodinate.

## Approach

The naive approach is to do a brute force on each coordinate where you see if it can reach both the atlantic and pacific, but this is inefficient.

The optimal approach is to start at the ocean. You take all the coordinates bordering the pacific and atlantic and put them in their respective sets. Then you will do a dfs on each of the border coordinates in the set just seeing what are the coordinates that can be reached from here.

The tricky part now is that since you are starting in the ocean then you will only add a node to the set if the height is greater than the one you are currently at instead of the other way around.

Once this is complete, you see the intersection of the sets and that is the coordinates that can reach both.

This reverse logic approach seems to be a pattern as it is what you had to do in rotting fruit as well.

## Code

```java
class Solution {
  public List<List<Integer>> pacificAtlantic(int[][] heights) {
    Set<List<Integer>> pac = new HashSet<>();
    Set<List<Integer>> atl = new HashSet<>();

    for (int c = 0; c < heights[0].length; ++c) {
      dfs(0, c, pac, heights[0][c], heights);
      dfs(heights.length - 1, c, atl, heights[heights.length - 1][c], heights);
    }

    for (int r = 0; r < heights.length; ++r) {
      dfs(r, 0, pac, heights[r][0], heights);
      dfs(r, heights[0].length - 1, atl, heights[r][heights[0].length - 1], heights);
    }

    List<List<Integer>> res = new ArrayList<>();
    for (int r = 0; r < heights.length; ++r) {
      for (int c = 0; c < heights[0].length; ++c) {
        List<Integer> coord = new ArrayList<>();
        coord.add(r);
        coord.add(c);

        if (pac.contains(coord) && atl.contains(coord)) {
          res.add(coord);
        }
      }
    }

    return res;
  }

  private void dfs(int r, int c, Set<List<Integer>> visit, int prevHeight, int[][] heights) {
    List<Integer> coord = new ArrayList<>();
    coord.add(r);
    coord.add(c);

    if (r < 0 || r >= heights.length || c < 0 || c >= heights[0].length || heights[r][c] < prevHeight || visit.contains(coord)) {
      return;
    }

    visit.add(coord);
    dfs(r + 1, c, visit, heights[r][c], heights);
    dfs(r - 1, c, visit, heights[r][c], heights);
    dfs(r, c + 1, visit, heights[r][c], heights);
    dfs(r, c - 1, visit, heights[r][c], heights);
  }
}
```

## Time Complexity

**Time Complexity**: O(m _ n)  
**Space Complexity**: O(m _ n)
