[Link](https://leetcode.com/problems/minimum-window-substring/)

```java
public class Solution {
    public String minWindow(String s, String t) {

        int[] cnt = new int[256];
        int unique = 0;
        for (char c : t.toCharArray()) {
            if (cnt[c] == 0) {
                unique++;
            }
            cnt[c]++;
        }
        int lo = -1; // exclusive
        int hi = -1;
        boolean expand = true;
        int min = s.length() + 1;
        String res = "";
        int[] obsCnt = new int[256];
        int obsUnique = 0;
        while (true) {
            if (expand) {
                hi++;
                if (hi == s.length()) {
                    break;
                }
                char c = s.charAt(hi);
                obsCnt[c]++;
                if (obsCnt[c] == cnt[c]) {
                    obsUnique++;
                }
                if (obsUnique == unique) {
                    expand = false;
                    if (hi - lo  < min) {
                        min = hi - lo;
                        res = s.substring(lo + 1, hi + 1);
                    }
                }
            } else {
                lo++;
                char c = s.charAt(lo);
                obsCnt[c]--;
                if (obsCnt[c] < cnt[c]) {
                    obsUnique--;
                    expand = true;
                }
                if (obsUnique == unique) {
                    if (hi - lo  < min) {
                        min = hi - lo;
                        res = s.substring(lo + 1, hi + 1);
                    }
                }
            }
        }
        return res;
    }
}
```
