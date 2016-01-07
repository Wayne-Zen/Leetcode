[Link](https://leetcode.com/problems/palindrome-partitioning-ii/)


```java
public class Solution {
    public int minCut(String s) {
        int len = s.length();
        boolean[][] isPalin = new boolean[len][len];
        for (int l = 1; l <= len; l++) {
            for (int i = 0; i + l - 1 < len; i++) {
                int j = i + l - 1;
                if (i == j
                        || (i + 1 == j && s.charAt(i) == s.charAt(j)) 
                        || (s.charAt(i) == s.charAt(j) && isPalin[i + 1][j - 1])) {
                    isPalin[i][j] = true;
                } 
            }
        }
        int[] dp = new int[len + 1];
        for (int i = 0; i < dp.length; i++) {
            dp[i] = i - 1; // 最多每个字符是一个palin，切n－1刀, dp[0] = -1;
        }
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 1; j <= i; j++) { // last part length
                if (isPalin[i - j][i - 1]) {
                    dp[i] = Math.min(dp[i], dp[i - j] + 1);
                }
            }
        }
        return dp[len];
    }
}
```
