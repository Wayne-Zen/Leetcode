[Link](https://leetcode.com/problems/word-break-ii/)

* 利用dp剪枝

```java
public class Solution {
    public List<String> wordBreak(String s, Set<String> wordDict) {
        int N = s.length();
        boolean[][] isWord = new boolean[N][N];
        for (int i = 0; i < N; i++) {
            for (int j = i; j < N; j++) {
                isWord[i][j] = wordDict.contains(s.substring(i, j + 1));
            }
        }
        
        boolean[] dp = new boolean[s.length() + 1];
        dp[s.length()] = true;
        for (int i = s.length() - 1; i >= 0; i--) {
            for (int j = i; j < s.length(); j++) {
                if (isWord[i][j] && dp[j + 1]) {
                    dp[i] = true;
                    break;
                }
            }
        }
        
        List<String>  res = new ArrayList<String>();
        List<Integer> now = new ArrayList<Integer>();
        help(res, now, isWord, dp, s, 0);
        return res;
    }
    
    private void help(List<String> res,
                      List<Integer> now,
                      boolean[][] isWord,
                      boolean[] dp,
                      String s, int start) {
        if (!dp[start]) {
            return;
        }
        if (start == s.length()) {
            StringBuilder sb = new StringBuilder();
            int begin = 0;
            for (int i = 0; i < now.size(); i++) {
                if (i != 0) {
                    sb.append(" ");
                }
                sb.append(s.substring(begin, now.get(i)));
                begin = now.get(i);
            }
            res.add(sb.toString());
            return;
        }
        for (int i = start; i < s.length(); i++) {
            if (!isWord[start][i]) {
                continue;
            }
            now.add(i + 1);
            help(res, now, isWord, dp, s, i + 1);
            now.remove(now.size() - 1);
        }
    }
    
    private List<String> parse(List<List<String>> res) {
        List<String> ret = new ArrayList<String>();
        for (List<String> sub : res) {
            StringBuilder sb = new StringBuilder();
            sb.append(sub.get(0));
            for (int i = 1; i < sub.size(); i++) {
                sb.append(' ');
                sb.append(sub.get(i));
            }
            ret.add(sb.toString());
        }
        return ret;
    }
}
```
