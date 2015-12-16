[Link](https://leetcode.com/problems/spiral-matrix/)

```java
public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        ArrayList<Integer> res = new ArrayList<Integer>();
        if(matrix == null || matrix.length == 0) {
            return res;
        }
        int m = matrix.length;
        int n = matrix[0].length;
        int r = 0;
        int c = 0;
        while (m > 0 && n > 0) {
            if (m == 1) {
                for (int i = 0; i < n; i++) {
                    res.add(matrix[r][c++]);
                }
                break;
            }
            if (n == 1) {
                for (int i = 0; i < m; i++) {
                    res.add(matrix[r++][c]);
                }
                break;
            }
            for (int i = 0; i < n - 1; i++) {
                res.add(matrix[r][c++]);
            }
            for (int i = 0; i < m - 1; i++) {
                res.add(matrix[r++][c]);
            }
            for (int i = 0; i < n - 1; i++) {
                res.add(matrix[r][c--]);
            }
            for (int i = 0; i < m - 1; i++) {
                res.add(matrix[r--][c]);
            }
            r++;
            c++;
            m -= 2;
            n -= 2;
        }
        return res;
    }
}
```
