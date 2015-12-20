[Link](https://leetcode.com/problems/strobogrammatic-number-ii/)

```java
public class Solution {
    public List<String> findStrobogrammatic(int n) {
        return helper(n, n);
    }
    public List<String> helper(int n, int len) {
        if (n == 0) return new ArrayList<String>(Arrays.asList(""));        
        if (n == 1) return new ArrayList<String>(Arrays.asList("0", "1", "8"));

        List<String> list = helper(n-2, len);
        List<String> res = new ArrayList<String>();
        for (String s : list) {
            if (n != len) res.add("0" + s + "0");
            res.add("1" + s + "1");
            res.add("8" + s + "8");
            res.add("6" + s + "9");
            res.add("9" + s + "6");             
        }
        return res;
    }
}
```

```java
public class Solution {
    public List<String> findStrobogrammatic(int n) {
        List<String> res = new ArrayList<String>();
        if (n == 0) {
            return res;
        }
        if (n == 1) {
            res.add("0");
            res.add("1");
            res.add("8");
            return res;
        }
        char[] cand = new char[]{'0', '1', '6', '8', '9'};
        
        boolean[] visited = new boolean[cand.length];
        help(res, "", visited, cand, n/2, n%2);
        return res;
    }
    private void help(List<String> res, String now,
                      boolean[] visited, char[] cand,
                      int n, int odd) { 
        if (now.length() == n) {
            String rev = buildRev(now);
            if (odd == 1) {
                res.add(now + "0" + rev);
                res.add(now + "1" + rev);
                res.add(now + "8" + rev);
            } else {
                res.add(now + rev);
            }
            return;
        }
        for (int i = 0; i < cand.length; i++) {
            if (now.length() == 0 && cand[i] == '0') {
                continue;
            }
            visited[i] = true;
            help(res, now + cand[i], visited, cand, n, odd);
            visited[i] = false;
        }
    }
    private String buildRev(String str) {
        StringBuilder sb = new StringBuilder();
        for (int i = str.length() - 1; i >= 0; i--) {
            if (str.charAt(i) == '6') {
                sb.append('9');
            } else if (str.charAt(i) == '9') {
                sb.append('6');
            } else {
                sb.append(str.charAt(i));
            }
        }
        return sb.toString();
    }
}
```
