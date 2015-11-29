[Link](https://leetcode.com/problems/basic-calculator-ii/)

```java
public class Solution {
    public int calculate(String s) {
        int sign = 1; //'+' = 1, '-' = -1
        int mulDiv = -1; //'none' = -1, '*' = 0, '/' = 1
        int res = 0;
        int preV = -1;
        for (int i = 0; i < s.length(); i++) {
            if (Character.isDigit(s.charAt(i))) {
                int num = s.charAt(i) - '0';
                while (++i < s.length() && Character.isDigit(s.charAt(i))) {
                    num = num * 10 + s.charAt(i) - '0';
                }
                i--;
                if (mulDiv == 0) {
                    preV *= num;
                    mulDiv = -1; //reset
                } else if (mulDiv == 1) {
                    preV /= num; 
                    mulDiv = -1; //reset
                } else {
                    preV = num;
                }
            }
            else if (s.charAt(i) == '+') {
                res += sign * preV; //previous sign 
                sign = 1; //current sign
            } else if (s.charAt(i) == '-') {
                res += sign * preV;
                sign = -1;
            } else if (s.charAt(i) == '*') {
                mulDiv = 0;
            } else if (s.charAt(i) == '/') {
                mulDiv = 1;
            }
        }
        res += sign * preV;
        return res;
    }
}
```
