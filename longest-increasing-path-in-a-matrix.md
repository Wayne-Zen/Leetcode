[Link](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)

```java
public class Solution {
    public int longestIncreasingPath(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int m = matrix.length;
        int n = matrix[0].length;
        int[][] cache = new int[m][n];
        int max = 1;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                max = Math.max(max, help(matrix, i, j, cache));
            }
        }
        return max;
    }
    int[] rAdd = {0, 0, 1, -1};
    int[] cAdd = {1, -1, 0, 0};
    private int help(int[][] matrix, int row, int col, int[][] cache) {
        if (cache[row][col] != 0) {
            return cache[row][col];
        }
        int m = matrix.length;
        int n = matrix[0].length;
        int max = 1;
        for (int i = 0; i < 4; i++) {
            int r = row + rAdd[i];
            int c = col + cAdd[i];
            if (r >= m || r < 0 || c >= n || c < 0 || matrix[r][c] <= matrix[row][col]) {
                continue;
            }
            int l = help(matrix, r, c, cache) + 1;
            max = Math.max(max, l);
        }
        cache[row][col] = max;
        return max;
    }
}
```
