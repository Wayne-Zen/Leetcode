[Link](https://leetcode.com/problems/restore-ip-addresses/)

* 先验证cnt，在验证s.length()
*  i < Math.min(3, s.length())


```java
public class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<String>();
        help(res, "", s, 0);
        return res;
    }
    private void help(List<String> res, String now, String s, int cnt) {
        if (cnt == 4) {
            if (s.length() == 0) {
                res.add(now);
            }
            return;
        }
        for (int i = 0; i < Math.min(3, s.length()); i++) {
            String prefix = s.substring(0, i + 1);
            String suffix = s.substring(i + 1);
            if (prefix.length() != 1 && prefix.charAt(0) == '0') {
                continue;
            }
            if (Integer.valueOf(prefix) > 255) {
                continue;
            }
            help(res, now + (now.length() == 0 ? "" : ".") + prefix, suffix, cnt + 1);
        }
    }
}
```
