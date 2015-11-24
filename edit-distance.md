[Link](https://leetcode.com/problems/edit-distance/)

```java
public class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length() + 1;
        int n = word2.length() + 1;
        int[][] dp = new int[m][n];
        dp[0][0] = 0;
        for (int i = 1; i < m; i++) {
            dp[i][0] = dp[i - 1][0] + 1;
        }
        for (int j = 1; j < n; j++) {
            dp[0][j] = dp[0][j - 1] + 1;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                int diag = word1.charAt(i - 1) == word2.charAt(j - 1) ? 
                           dp[i - 1][j - 1] : dp[i - 1][j - 1] + 1;
                int up = dp[i][j - 1] + 1;
                int left = dp[i - 1][j] + 1;
                dp[i][j] = Math.min(diag, Math.min(up, left));
            }
        }
        return dp[m - 1][n - 1];
    }
}
```
