[Link](https://leetcode.com/problems/unique-binary-search-trees/)

```java
public class Solution {
    //f(0) = 1
    //f(n) = f(0)*f(n-1) + f(1)*f(n-2) + ... + f(n-2)*f(1) + f(n-1)*f(0)
    public int numTrees(int N) {
        int[] dp = new int[N + 1];
        dp[0] = 1;
        for (int n = 1; n <= N; n++) {
            for (int k = 0; k < n; k++) {
                dp[n] += dp[k] * dp[n - 1 - k];
            }
        }
        return dp[N];
    }
}
```
