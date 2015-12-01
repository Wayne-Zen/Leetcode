[Link](https://leetcode.com/problems/sparse-matrix-multiplication/)

```java
public class Solution {
    public int[][] multiply(int[][] A, int[][] B) {
        boolean[] zeroRow = new boolean[A.length];
        boolean[] zeroCol = new boolean[B[0].length];
        for (int i = 0; i < A.length; i++) {
            boolean allZero = true;
            for (int j = 0; j < A[0].length; j++) {
                if (A[i][j] != 0) {
                    allZero = false;
                }
            }
            zeroRow[i] = allZero;
        }
        for (int j = 0; j < B[0].length; j++) {
            boolean allZero = true;
            for (int i = 0; i < B.length; i++) {
                if (B[i][j] != 0) {
                    allZero = false;
                }
            }
            zeroCol[j] = allZero;
        }
        int[][] res = new int[A.length][B[0].length];
        for (int i = 0; i < A.length; i++) {
            for (int j = 0; j < B[0].length; j++) {
                if (zeroRow[i] || zeroCol[j]) {
                    res[i][j] = 0;
                } else {
                    int sum = 0;
                    for (int k = 0; k < A[0].length; k++) {
                        sum += A[i][k] * B[k][j];
                    }
                    res[i][j] = sum;
                }
            }
        }
        return res;
    }
}
```
