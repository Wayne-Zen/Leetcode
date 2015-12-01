[Link](https://leetcode.com/problems/basic-calculator-ii/)

```java
public class Solution {
    public int calculate(String s) {
        s = " " + s + " ";
        int curVal = 0;
        int preVal = 0;
        int sum = 0;
        char op = '+';
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                while (Character.isDigit(c)) {
                    curVal = curVal * 10 + c - '0';
                    c = s.charAt(++i);
                }
                if (op == '+') {
                    preVal = curVal;
                } else if (op == '-') {
                    preVal = -curVal;
                } else if (op == '*') {
                    sum -= preVal;
                    preVal = preVal * curVal;
                } else if (op == '/') {
                    sum -= preVal;
                    preVal = preVal / curVal;
                }
                sum += preVal;
                curVal = 0;
            }
            if (c != ' ') {
                op = c;
            }
        }
        return sum;
    }
}
```
