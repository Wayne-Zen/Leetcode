[Link](https://leetcode.com/problems/range-sum-query-2d-immutable/)

```java
public class NumMatrix {
    int[][] sum;
    
    public NumMatrix(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }
        int m = matrix.length + 1;
        int n = matrix[0].length + 1;
        sum = new int[m][n];
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                sum[i][j] = sum[i - 1][j]
                          + sum[i][j - 1]
                          - sum[i - 1][j - 1] // 坑
                          + matrix[i - 1][j - 1];
                
            }
        }
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        return sum[row2 + 1][col2 + 1] 
                - sum[row2 + 1][col1] 
                - sum[row1][col2 + 1] 
                + sum[row1][col1];
    }
}


// Your NumMatrix object will be instantiated and called as such:
// NumMatrix numMatrix = new NumMatrix(matrix);
// numMatrix.sumRegion(0, 1, 2, 3);
// numMatrix.sumRegion(1, 2, 3, 4);
```
