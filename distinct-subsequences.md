[Link](https://leetcode.com/problems/distinct-subsequences/)

```java
public class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length() + 1;
        int n = t.length() + 1;
        int[][] dp = new int[m][n];
        dp[0][0] = 1;
        for (int i = 1; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int j = 1; j < n; j++) {
            dp[0][j] = 0;
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < Math.min(n, i + 1); j++) { //优化
                int add = 0;
                if (s.charAt(i - 1) == t.charAt(j - 1)) {
                    add = dp[i - 1][j - 1];
                }
                dp[i][j] = dp[i - 1][j] + add;
            }
        }
        return dp[m - 1][n - 1];
    }
}
```
