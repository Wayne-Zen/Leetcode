[Link](https://leetcode.com/problems/word-break/)

```java
public class Solution {
    public boolean wordBreak(String s, Set<String> wordDict) {
        int N = s.length();
        boolean[] dp = new boolean[N + 1];
        dp[0] = true;
        for (int i = 1; i <= N; i++) {
            boolean attemp = false;
            for (int j = 0; j < i; j++) {
                attemp = dp[j] && wordDict.contains(s.substring(j, i));
                if (attemp) {
                    break;
                }
            }
            dp[i] = attemp;
        }
        return dp[N];
    }
}
```
