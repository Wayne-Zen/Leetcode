[Link](https://leetcode.com/problems/decode-ways/)

```java
public class Solution {
    public int numDecodings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        int n = s.length();
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = Integer.valueOf(s.substring(0, 1)) > 0 ? 1 : 0;
        for (int i = 2; i < dp.length; i++) {
            if (Integer.valueOf(s.substring(i - 1, i)) > 0) {
                dp[i] += dp[i - 1];
            }
            if (Integer.valueOf(s.substring(i - 2, i)) >= 10 && Integer.valueOf(s.substring(i - 2, i)) <= 26) {
                dp[i] += dp[i - 2];
            }
        }
        return dp[n];
    }
}
```
