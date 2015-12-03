[Link](https://leetcode.com/problems/one-edit-distance/)

```java
public class Solution {
    public boolean isOneEditDistance(String s, String t) {
        if (Math.abs(s.length() - t.length()) > 1) {
            return false;
        }
        if (s.equals(t)) {
            return false;
        }
        if (s.length() == t.length()) {
            int cnt = 0;
            for (int i = 0; i < s.length(); i++) {
                if (s.charAt(i) != t.charAt(i)) {
                    cnt++;
                    if (cnt > 1) {
                        return false;
                    }
                }
            }
            return cnt == 1;
        } else {
            String s1 = s.length() < t.length() ? s : t;//short
            String s2 = s.length() < t.length() ? t : s;//long
            for (int i = 0; i < s2.length(); i++) {
                if (s1.equals(s2.substring(0, i) + s2.substring(i + 1))) {
                    return true;
                }
            }
            return false;
        }
    }
}
```
