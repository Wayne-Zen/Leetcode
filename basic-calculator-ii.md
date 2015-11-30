[Link](https://leetcode.com/problems/basic-calculator-ii/)

```java
public class Solution {
    public int calculate(String s) {
        s = " " + s + " ";
        int curVal = 0;
        int preVal = 0;
        int sum = 0;
        int op = 0; // + - * /
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                while (Character.isDigit(c)) {
                    curVal = curVal * 10 + c - '0';
                    c = s.charAt(++i);
                }
                if (op == 0) {
                    preVal = curVal;
                } else if (op == 1) {
                    preVal = -curVal;
                } else if (op == 2) {
                    sum -= preVal;
                    preVal = preVal * curVal;
                } else if (op == 3) {
                    sum -= preVal;
                    preVal = preVal / curVal;
                }
                sum += preVal;
                curVal = 0;
            }
            if (c == '+') {
                op = 0;
            } else if (c == '-') {
                op = 1;
            } else if (c == '*') {
                op = 2;
            } else if (c == '/') {
                op = 3;
            }
        }
        return sum;
    }
}
```
