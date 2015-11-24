[Link](https://leetcode.com/problems/search-a-2d-matrix/)

```java
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;
        int lo = 0;
        int hi = m * n - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (matrix[mid/n][mid%n] == target) {
                return true;
            } else if (matrix[mid/n][mid%n] < target) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        if (matrix[lo/n][lo%n] == target) {
            return true;
        } else if (matrix[hi/n][hi%n] == target) {
            return true;
        } else {
            return false;
        }
    }
}
```
