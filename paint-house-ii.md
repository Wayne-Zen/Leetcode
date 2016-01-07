[Link](https://leetcode.com/problems/paint-house-ii/)

```java
public class Solution {
    public int minCostII(int[][] costs) {
        if (costs == null || costs.length == 0) {
            return 0;
        }
        int h = costs.length;
        int k = costs[0].length;
        // house i 涂颜色 j， 最小cost
        int[][] dp = new int[h][k];
        for (int i = 0; i < k; i++) {
            dp[0][i] = costs[0][i];
        }
        for (int i = 1; i < h; i++) {
            int min1 = Integer.MAX_VALUE; // 最小
            int min2 = Integer.MAX_VALUE; // 次小
            int index1 = 0;
            int index2 = 0;
            if (dp[i - 1][0] < dp[i - 1][1]) {
                min1 = dp[i - 1][0];
                min2 = dp[i - 1][1];
                index1 = 0;
                index2 = 1;
            } else {
                min1 = dp[i - 1][1];
                min2 = dp[i - 1][0];
                index1 = 1;
                index2 = 0;
            }
            for (int j = 2; j < k; j++) {
                if (dp[i - 1][j] < min1) {
                    min2 = min1;
                    index2 = index1;
                    min1 = dp[i - 1][j];
                    index1 = j;
                } else if (dp[i - 1][j] < min2) {
                    min2 = dp[i - 1][j];
                    index2 = j;
                }
            }
            for (int j = 0; j < k; j++) {
                if (j == index1) {
                    dp[i][j] = costs[i][j] + min2;
                } else {
                    dp[i][j] = costs[i][j] + min1;
                }
            }
        }
        int res = Integer.MAX_VALUE;
        for (int i = 0; i < k; i++) {
            res = Math.min(res, dp[h - 1][i]);
        }
        return res;
    }
}
```
