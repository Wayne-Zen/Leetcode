[Link](https://leetcode.com/problems/paint-house-ii/)

```java
public class Solution {
    public int minCostII(int[][] costs) {
        if (costs == null || costs.length == 0) {
            return 0;
        }
        int h = costs.length;
        int k = costs[0].length;
        
        int min1 = Integer.MAX_VALUE; // 最小
        int min2 = Integer.MAX_VALUE; // 次小
        int index1 = 0;
        int index2 = 0;
        // house i 涂颜色 j， 最小cost
        int[][] dp = new int[h][k];
        for (int j = 0; j < k; j++) {
            dp[0][j] = costs[0][j];
            if (dp[0][j] < min1) {
                min2 = min1;
                index2 = index1;
                min1 = dp[0][j];
                index1 = j;
            } else if (dp[0][j] < min2) {
                min2 = dp[0][j];
                index2 = j;
            }
        }
        for (int i = 1; i < h; i++) {
            int oldmin1 = min1;
            int oldmin2 = min2;
            int oldminIndex = index1;
            min1 = Integer.MAX_VALUE; // 最小
            min2 = Integer.MAX_VALUE; // 次小
            index1 = 0;
            index2 = 0;
            for (int j = 0; j < k; j++) {
                if (j == oldminIndex) {
                    dp[i][j] = costs[i][j] + oldmin2;
                } else {
                    dp[i][j] = costs[i][j] + oldmin1;
                }
                // update min
                if (dp[i][j] < min1) {
                    min2 = min1;
                    index2 = index1;
                    min1 = dp[i][j];
                    index1 = j;
                } else if (dp[i][j] < min2) {
                    min2 = dp[i][j];
                    index2 = j;
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
