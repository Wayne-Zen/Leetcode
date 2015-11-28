[Link](https://leetcode.com/problems/search-a-2d-matrix-ii/)

```java
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;
        int r = m - 1;
        int c = 0;
        while (r >= 0 && c < n) {
            if (target == matrix[r][c]) {
                return true;
            } else if (target > matrix[r][c]) {
                c++;
            } else {
                r--;
            }
        }
        return false;
    }
}
```
