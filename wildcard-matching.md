[Link](https://leetcode.com/problems/wildcard-matching/)

[https://www.zybuluo.com/wayne-zen/note/144290](https://www.zybuluo.com/wayne-zen/note/144290)

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        int M = s.length() + 1;
        int N = p.length() + 1;
        boolean[][] dp = new boolean[M][N];
        dp[0][0] = true;
        for (int j = 1; j < N; j++) {
            dp[0][j] = p.charAt(j - 1) == '*' && dp[0][j - 1];
        }
        for (int i = 1; i < M; i++) {
            for (int j = 1; j < N; j++) {
                if (s.charAt(i - 1) == p.charAt(j - 1) || p.charAt(j - 1) == '?') {
                    dp[i][j] = dp[i - 1][j - 1];    
                } else if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                } else {
                    dp[i][j] = false;
                }
            }
        }
        return dp[M - 1][N - 1];
    }
}
```
