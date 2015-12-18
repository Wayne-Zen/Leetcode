[Link](https://leetcode.com/problems/basic-calculator/)

```java
public class Solution {
    public int calculate(String s) {
        Stack<Integer> num = new Stack<Integer>();
        Stack<Character> op = new Stack<Character>();
        int val = 0;
        boolean numFlag = false;
        s = "(" + s + ")";
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                while (Character.isDigit(c)) {
                    val = val * 10 + c - '0';
                    c = s.charAt(++i);
                }
                i--;
                num.push(val);
                val = 0;
            } else if (c == '(' || c == '+' || c == '-') {
                op.push(c);
            } else if (c == ')') {
                int temp = 0;
                while (op.peek() != '(') {
                    char o = op.pop();
                    int v = num.pop();
                    if (o == '-') {
                        temp += -v;
                    } else if (o == '+') {
                        temp += v;
                    }
                }
                num.push(num.pop() + temp);
                op.pop();
            }
        }
        return num.pop();
    }
}
```
