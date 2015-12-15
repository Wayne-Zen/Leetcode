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
        dfs(s, "", res, dict);
        return res;
    }

    public void dfs(String s, String now, List<String> res, Set<String> dict)  {
        if (s.length() == 0) {
            res.add(new String(now));
            return;
        }
        for (int i = 0; i < s.length(); i++) {
            String sub = s.substring(0, i + 1);
            String rest = s.substring(i + 1);
            if (!dict.contains(sub)) {
                continue;
            }
            dfs(rest, now + (now.length() == 0 ? "" : " ") + sub, res, dict);
        }
    }
}

```

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
        HashMap<String, List<String>> map = new HashMap<String, List<String>>();
        return dfs(s, dict, map);
    }

    public List<String> dfs(String s, Set<String> dict,
                    HashMap<String, List<String>> map)  {
        List<String> res = new ArrayList<String>();
        if (dict.contains(s)) {
            res.add(s);
        }
        for (int i = 0; i < s.length(); i++) {
            String prefix = s.substring(0, i + 1);
            String suffix = s.substring(i + 1);
            if (!dict.contains(prefix)) {
                continue;
            }
            List<String> suffixRes = null;
            if (map.containsKey(suffix)) {
                suffixRes = map.get(suffix);
            } else {
                suffixRes = dfs(suffix, dict, map);
            }
            for (String str : suffixRes) {
                res.add(prefix + " " + str);
            }
        }
        map.put(s, res);
        return res;
    }
}
```
