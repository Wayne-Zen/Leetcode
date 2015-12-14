[Link](https://leetcode.com/problems/word-break/)

```java
public class Solution {
    public boolean wordBreak(String s, Set<String> wordDict) {
        int N = s.length() + 1;
        boolean[] dp = new boolean[N];
        dp[0] = true;
        for (int i = 1; i < N; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordDict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[N - 1];
    }
}
```
