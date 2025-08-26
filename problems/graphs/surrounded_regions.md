# Surrounded Regions

**Link:** (https://neetcode.io/problems/surrounded-regions?list=neetcode150)  
**Difficulty:** Medium  
**Date Solved:** 8/25/25  
**Category:** Graphs

## Problem Statement

You are given a grid of X's and O's, if a continous group of O's is unable to reach the border of the grid and is surrounded by X's, then it is considered surrounded. Change all of the surrounded O's to X's in-place.

## Approach

My first approach was to find the O's that weren't on the border and then see if they were unable to reach the border, this quickly became complicated and the classic graph solution of reverse logic worked much better.

Every O on the border wasn't surrounded, so if you started at an O on the border and searched for the O's it was connected to you, then you could find all the ones that weren't surrounded. Then that means everything else is surrounded.

So you check every border element for if it's an O then you do a searching algo on that element to see what other O's it's connected to, then you run through every graph element and change every element that wasn't searched for to an X.

## Code

```java
class Solution {
    int[][] DIRECTIONS = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    public void solve(char[][] board) {
        for (int r = 0; r < board.length; ++r) {
            if (board[r][0] == 'O') {
                bfs(board, r, 0);
            }
            if (board[r][board[0].length - 1] == 'O') {
                bfs(board, r, board[0].length - 1);
            }
        }

        for (int c = 0; c < board[0].length; ++c) {
            if (board[0][c] == 'O') {
                bfs(board, 0, c);
            }
            if (board[board.length - 1][c] == 'O') {
                bfs(board, board.length - 1, c);
            }
        }

        for (int r = 0; r < board.length; ++r) {
            for (int c = 0; c < board[0].length; ++c) {
                if (board[r][c] == '#') {
                    board[r][c] = 'O';
                } else {
                    board[r][c] = 'X';
                }
            }
        }
    }

    private void bfs(char[][] board, int r, int c) {
        Queue<int[]> q = new LinkedList<>();
        q.add(new int[]{r, c});
        board[r][c] = '#';

        while(!q.isEmpty()) {
                int[] coord = q.poll();

                for (int[] DIR: DIRECTIONS) {
                    int nr = coord[0] + DIR[0];
                    int nc = coord[1] + DIR[1];

                    if ((nr < board.length) && nr >= 0 && (nc < board[0].length) &&
                        nc >= 0 && board[nr][nc] != '#' && board[nr][nc] == 'O') {
                        q.add(new int[]{nr, nc});
                        board[nr][nc] = '#';
                    }
                }
        }
    }
}
```

## Time Complexity

**Time Complexity**: O(m _ n)  
**Space Complexity**: O(m _ n)
