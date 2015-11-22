[Link](https://leetcode.com/problems/rotate-image/)

* rotate n-1 array

```java
public class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for (int level = 0; level < n / 2; level++) {
            int[] temp = new int[n];
            for (int i = level; i < n - 1 - level; i++) {
                temp[i] = matrix[level][i];
                matrix[level][i] = matrix[n - 1 - i][level];
                matrix[n - 1 - i][level] = matrix[n - 1 - level][n - 1 - i];
                matrix[n - 1 - level][n - 1 - i] = matrix[i][n - 1 - level];
                matrix[i][n - 1 - level] = temp[i];
            }
        }
    }
}
```
