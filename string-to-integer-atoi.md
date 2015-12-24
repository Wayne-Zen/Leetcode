[Link](https://leetcode.com/problems/string-to-integer-atoi/)

```java
public class Solution {
    public int myAtoi(String str) {
        if (str == null) {
            return 0;
        }
        str = str.trim();
        if (str.length() == 0) {
            return 0;
        }
        int flag = 1;
        if (str.charAt(0) == '+') {
            str = str.substring(1);
        } else if (str.charAt(0) == '-') {
            str = str.substring(1);
            flag = -1;
        }
        double val = 0;
        for (int i = 0; i < str.length(); i++) {
            char c = str.charAt(i);
            if (!Character.isDigit(c)) {
                break;
            }
            val = val * 10 + c - '0';
        }
        val = val * flag;
        if (val > Integer.MAX_VALUE) {
            return Integer.MAX_VALUE;
        } else if (val < Integer.MIN_VALUE) {
            return Integer.MIN_VALUE;
        } else {
            return (int)val;
        }
    }
}
```
