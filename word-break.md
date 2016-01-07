[Link](https://leetcode.com/problems/word-break/)

```java
public class Solution {
    public boolean wordBreak(String s, Set<String> wordDict) {
        int n = s.length() + 1;
        boolean[] dp = new boolean[n];
        dp[0] = true;
        for (int i = 1; i < n; i++) {
            for (int j = 1; j <= i; j++) { // last part length
                if (dp[i - j] && wordDict.contains(s.substring(i - j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[n - 1];
    }
}
```
