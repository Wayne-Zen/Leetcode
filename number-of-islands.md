[Link](https://leetcode.com/problems/number-of-islands/)

```java
public class Solution {
    public int numIslands(char[][] grid) {
        int res = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    grid[i][j] = '0';
                    bfs(grid, i, j);
                    res++;
                }
            }
        }
        return res;
    }
    private void bfs(char[][] grid, int row, int col) {
        int m = grid.length;
        int n = grid[0].length;
        int[] rAdd = {1, -1, 0, 0};
        int[] cAdd = {0, 0, 1, -1};
        Queue<Integer> q = new LinkedList<Integer>();
        q.offer(row * n + col);
        while (!q.isEmpty()) {
            int loc = q.poll();
            row = loc / n;
            col = loc % n;
            for (int i = 0; i < 4; i++) {
                int r = row + rAdd[i];
                int c = col + cAdd[i];
                if (r >= 0 && r < m && c >= 0 && c < n 
                        && grid[r][c] == '1') {
                    grid[r][c] = '0';
                    q.offer(r * n + c);    
                }
            }
        }
    } 
}
```
