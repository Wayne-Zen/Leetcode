[Link](https://leetcode.com/problems/burst-balloons/)

```java
public class Solution {
    public int maxCoins(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int N = nums.length;
        int[][] dp = new int[N][N];
        for (int len = 1; len <= N; len++) {
            for (int i = 0; i + len - 1 < N; i++) {
                int j = i + len - 1;
                int max = 0;
                for (int k = i; k <= j; k++) {
                    int val = nums[k]
                             * (i - 1 >= 0 ? nums[i - 1] : 1)
                             * (j + 1 < N ? nums[j + 1] : 1) 
                             + (k - 1 >= i ? dp[i][k - 1] : 0)
                             + (k + 1 <= j ? dp[k + 1][j] : 0);
                    max = Math.max(max, val);
                }
                dp[i][j] = max;
            }
        }
        return dp[0][N - 1];
    }
}
```
