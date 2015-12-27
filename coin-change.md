[Link](https://leetcode.com/problems/coin-change/)

```java
public class Solution {
    public int coinChange(int[] coins, int amount) {
        Arrays.sort(coins);
        int M = coins.length; 
        int N = amount + 1;
        int[][] dp = new int[M][N];
        for (int j = 0; j < N; j++) {
            if (j % coins[0] == 0) {
                dp[0][j] = j / coins[0];
            } else {
                dp[0][j] = -1;
            }
        }
        for (int i = 1; i < M; i++) {
            for (int j = 0; j < N; j++) {
                // coins[i]: coin value;
                // j: total;
                // dp[i][j]: num of coin
                int val = coins[i];
                long min = Long.MAX_VALUE;
                for (int k = 0; k <= j / val; k++) {
                    if (dp[i - 1][j - k * val] != -1) {
                        min = Math.min(min, k + dp[i - 1][j - k * val]);
                    }
                }
                if (min == Long.MAX_VALUE) {
                    dp[i][j] = -1;
                } else {
                    dp[i][j] = (int)min;
                }
            }
        }
        return dp[M - 1][N - 1];
    }
}
```
