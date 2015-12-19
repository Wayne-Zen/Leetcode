[Link](https://leetcode.com/problems/shortest-distance-from-all-buildings/)

```java
public class Solution {
    public int shortestDistance(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return -1;
        }
        int m = grid.length;
        int n = grid[0].length;
        int[][] dist = new int[m][n];
        int[][] reach = new int[m][n];
        
        int buildingNum = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    buildingNum++;
                    bfs(i, j, grid, dist, reach);
                }
            }
        }
        int min = Integer.MAX_VALUE;
        for (int i = 0; i< m; i++) {
            for (int j = 0; j < n; j++) {
                if (reach[i][j] == buildingNum) {
                    min = Math.min(min, dist[i][j]);
                }
            }
        }
        if (min == Integer.MAX_VALUE) {
            return -1;
        }
        return min;
    }
    
    private void bfs(int startRow, int startCol, int[][] grid, 
                     int[][] dist, int [][] reach) {
        int m = grid.length;
        int n = grid[0].length;
        Queue<Integer> q = new LinkedList<Integer>();
        q.offer(startRow * n + startCol);
        int[][] move = new int[m][n];
        int[] rAdd = {1, -1, 0, 0};
        int[] cAdd = {0, 0, 1, -1};
        while (!q.isEmpty()) {
            int loc = q.poll();
            int row = loc / n;
            int col = loc % n;
            for (int i = 0; i < 4; i++) {
                int r = row + rAdd[i];
                int c = col + cAdd[i];
                if (r < 0 || r >= m || c < 0 || c >= n 
                        || grid[r][c] != 0 || move[r][c] != 0) {
                    continue;
                }
                move[r][c] = move[row][col] + 1;
                q.offer(r * n + c);
                dist[r][c] += move[r][c];
                reach[r][c] += 1;
            }
        }
    }
}
```
