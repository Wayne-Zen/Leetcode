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
        int max = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                max = Math.max(max, help(matrix, cache, i, j));
            }
        }
        return max;
    }
    private int help(int[][] matrix, int[][] cache, int row, int col) {
        if (cache[row][col] != 0) {
            return cache[row][col];
        }
        int[] rAdd = new int[]{0, 0, 1, -1};
        int[] cAdd = new int[]{1, -1, 0, 0};
        int max = 1;
        for (int i = 0; i < 4; i++) {
            int r = row + rAdd[i];
            int c = col + cAdd[i];
            if (r < 0 || r >= matrix.length || c < 0 || c >= matrix[0].length || matrix[r][c] <= matrix[row][col]) {
                continue;
            }
            max = Math.max(1 + help(matrix, cache, r, c), max);
        }
        cache[row][col] = max;
        return cache[row][col];
    }
}
```
