[Link](https://leetcode.com/problems/palindrome-partitioning-ii/)


```java
public class Solution {
    public boolean[][] getTable(String s) {
        int N = s.length();
        boolean[][] table = new boolean[N][N];
        // len == 1
        for (int i = 0; i < N; i++) {
            table[i][i] = true;
        }
        // len == 2
        for (int i = 1; i < N; i++) {
            table[i - 1][i] = (s.charAt(i - 1) == s.charAt(i));
        }
        for (int len = 3; len <= N; len++) {
            for (int start = 0; start + len - 1 < N; start++) {
                table[start][start + len - 1] = table[start + 1][start + len - 2] 
                                            && s.charAt(start) == s.charAt(start + len - 1);
            }
        }
        return table;
    }
    public int minCut(String s) {
        int N = s.length();
        boolean[][] table = getTable(s);
        int[] dp = new int[N + 1];
        //dp[0] = -1; // 重要
        for (int i = 0; i < dp.length; i++) {
            dp[i] = i - 1; // 最多每个字符是一个palin，切n－1刀 
        }
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (table[j][i - 1]) {
                    dp[i] = Math.min(dp[i], dp[j] + 1);
                }
            }
        }
        return dp[N];
    }
    private boolean isPalin(String s, int lo, int hi) {
        while (lo < hi) {
            if (s.charAt(lo) != s.charAt(hi)) {
                return false;
            } else {
                lo++;
                hi--;
            }
        }
        return true;
    }
}
```
