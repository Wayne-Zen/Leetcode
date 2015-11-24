[Link](https://leetcode.com/problems/restore-ip-addresses/)

1. s[i]
2. s[i : i+1]，s[i] !=0时
3. s[i : i+2]，s[i] != 0，且s[i : i+2] <= 255


```java
public class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<List<String>> res = new ArrayList<List<String>>();
        List<String> now = new ArrayList<String>();
        help(res, now, s, 0);
        return parse(res);
    }
    private List<String> parse(List<List<String>> res) {
        List<String> out = new ArrayList<String>();
        for (int i = 0; i < res.size(); i++) {
            List<String> sub = res.get(i);
            StringBuilder sb = new StringBuilder();
            sb.append(sub.get(0));
            for (int j = 1; j < sub.size(); j++) {
                sb.append('.');
                sb.append(sub.get(j));
            }
            out.add(sb.toString());
        }
        return out;
    }
    private void help(List<List<String>> res,
                      List<String> now,
                      String s, int pos) {
        if (now.size() == 4) {
            if (pos == s.length()) {
                res.add(new ArrayList<String>(now));
            }
            return;
        }
        for (int i = 1; i <= 3; i++) {
            if (pos + i > s.length()) {
                continue;
            }
            String sub = s.substring(pos, pos + i);
            if (i == 2 && s.charAt(pos) == '0') {
                continue;
            }
            if (i == 3) {
                if (s.charAt(pos) == '0' || Integer.valueOf(sub) > 255) {
                    continue;
                }
            }
            now.add(sub);
            help(res, now, s, pos + i);
            now.remove(now.size() - 1);
        }
    }
}
```
