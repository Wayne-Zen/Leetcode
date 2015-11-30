[Link](https://leetcode.com/problems/burst-balloons/)

```java
public class Solution {
    public int maxCoins(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int N = nums.length;
        int[][] dp = new int[N][N];
        // 对角线一层层往右上角走
        // 想象k是最后一个爆的，而不是第一个
        for (int level = 0; level < N; level++) {
            int i = 0;
            int j = level;
            for (int depth = 0; depth < N - level; depth++) {
                int max = 0;
                for (int k = i; k <= j; k++) {
                    int v1 = i - 1 < 0 ? 1 : nums[i - 1];
                    int v2 = nums[k];
                    int v3 = j + 1 >= N ? 1 : nums[j + 1];
                    int d1 = k - 1 < i ? 0 : dp[i][k - 1];
                    int d2 = k + 1 > j ? 0 : dp[k + 1][j];
                    max = Math.max(max, v1 * v2 * v3 + d1 + d2);
                }
                dp[i][j] = max;
                i++;
                j++;
            }
        }
        return dp[0][N - 1];
    }
}
```
