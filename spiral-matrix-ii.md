[Link](https://leetcode.com/problems/spiral-matrix-ii/)

* 注意当n为奇数时， 填补最后的空

```java
public class Solution {
    public int[][] generateMatrix(int n) {
        int[][] matrix = new int[n][n];
        int r = 0;
        int c = 0;
        int val = 1;
        while (n > 0) {
            if (n == 1) {
                matrix[r][c] = val;
                break;
            }
            for (int i = 0; i < n - 1; i++) {
                matrix[r][c++] = val++;
            }
            for (int i = 0; i < n - 1; i++) {
                matrix[r++][c] = val++;
            }
            for (int i = 0; i < n - 1; i++) {
                matrix[r][c--] = val++;
            }
            for (int i = 0; i < n - 1; i++) {
                matrix[r--][c] = val++;
            }
            r++;
            c++;
            n -= 2;
        }
        return matrix;
    }
}
```
