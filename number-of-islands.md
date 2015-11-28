[Link](https://leetcode.com/problems/number-of-islands/)

```java
public class Solution {
    public int numIslands(char[][] grid) {
        int res = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                res += bfs(grid, i, j);
            }
        }
        return res;
    }
    private int bfs(char[][] grid, int r, int c) {
        if (grid[r][c] != '1') {
            return 0;
        }
        int N = grid[0].length;
        Queue<Integer> q = new LinkedList<Integer>();
        grid[r][c] = '0';
        q.offer(r * N + c);
        while (!q.isEmpty()) {
            int loc = q.poll();
            int row = loc / N;
            int col = loc % N;
            
            int[] nRow = new int[]{row + 1, row - 1, row, row};
            int[] nCol = new int[]{col, col, col + 1, col - 1};
            for (int i = 0; i < 4; i++) {
                if (nRow[i] >= 0 && nRow[i] < grid.length
                        && nCol[i] >= 0 && nCol[i] < grid[0].length
                        && grid[nRow[i]][nCol[i]] == '1') {
                    grid[nRow[i]][nCol[i]] = '0';
                    q.offer(nRow[i] * N + nCol[i]);
                }
            }
        }
        return 1;
    }
}
```
