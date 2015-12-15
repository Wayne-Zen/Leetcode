[Link](https://leetcode.com/problems/word-break-ii/)

* 利用dp剪枝

```java
public class Solution {
    public List<String> wordBreak(String s, Set<String> dict) {
        List<String> res = new ArrayList<String>();
        int N = s.length() + 1;
        boolean[] dp = new boolean[N];
        dp[0] = true;
        for (int i = 1; i < N; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                }
            }
        }
        if (dp[N - 1] == false) {
            return res; //DP的作用就这一行！！！
        }
        dfs(s, 0, "", res, dict);
        return res;
    }

    public void dfs(String s, int pos, String now, List<String> res, Set<String> dict)  {
        if (pos == s.length()) {
            res.add(new String(now));
            return;
        }
        for (int i = pos; i < s.length(); i++) {
            String sub = s.substring(pos, i + 1);
            if (!dict.contains(sub)) {
                continue;
            }
            dfs(s, i + 1, now + (now.length() == 0 ? "" : " ") + sub, res, dict);
        }
    }
}
```
