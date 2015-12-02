[Link](https://leetcode.com/problems/valid-number/)

```java
public class Solution {
    public boolean isNumber(String s) {
        s = s.trim();
        if (s.length() != 0 &&
                (s.charAt(0) == '+' || s.charAt(0) == '-')) {
            s = s.substring(1);
        }
        boolean num = false;
        boolean dot = false;
        boolean exp = false;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                num = true;
            } else if (c == '.') {
                if (exp || dot) {
                    return false;
                }
                dot = true;
            } else if (c == 'e') {
                // ".e1"
                if (!num || exp) {
                    return false;
                }
                exp = true;
                num = false;
            } else if (c == '+' || c == '-') {
                if (i == 0 || s.charAt(i - 1) != 'e') {
                    return false;
                }
            } else {
                return false;
            }
        }
        return num;
    }
}
```
