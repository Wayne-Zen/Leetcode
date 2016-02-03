[Link](https://leetcode.com/problems/coin-change/)

```java
public class Solution {
    // dp[x + c] = min(dp[x] + 1, dp[x + c])
    // 其中dp[x]代表凑齐金额x所需的最少硬币数，c为可用的硬币面值
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, -1);
        dp[0] = 0;
        for (int x = 0; x < amount; x++) {
            if (dp[x] == -1) {
                continue;
            }
            for (int c : coins) {
                if (x + c > amount) {
                    continue;
                }
                if (dp[x + c] == -1 || dp[x + c] > dp[x] + 1) {
                    dp[x + c] = dp[x] + 1;
                }
            }
        }
        return dp[amount];
    }
}
```

```java
public class Solution {
    public int coinChange(int[] coins, int amount) {
        int m = coins.length + 1;
        int n = amount + 1;
        int[][] dp = new int[m][n];
        for (int j = 1; j < n; j++) {
            dp[0][j] = -1;
        }
        for (int i = 1; i < m; i++) {
            int val = coins[i - 1];
            for (int j = 1; j < n; j++) {
                int target = j;
                // k current val
                dp[i][j] = Integer.MAX_VALUE;
                for (int k = target / val; k >= 0; k--) {
                    // rest val is target - k * val;
                    if (dp[i - 1][target - k * val] != -1) {
                        dp[i][j] = Math.min(dp[i][j], k + dp[i - 1][target - k * val]);
                    }
                }
                if (dp[i][j] == Integer.MAX_VALUE) {
                    dp[i][j] = -1;
                }
            }
        }
        return dp[m - 1][n - 1];
    }
}
```
