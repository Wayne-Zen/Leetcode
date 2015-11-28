[Link](https://leetcode.com/problems/basic-calculator/)

```java
public class Solution {
    public int calculate(String s) {
        Stack<Integer> num = new Stack<Integer>();
        Stack<Character> op = new Stack<Character>();
        Stack<Integer> numR = new Stack<Integer>();
        Stack<Character> opR = new Stack<Character>();
        StringBuilder sb = new StringBuilder();
        for (int i = -1; i <= s.length(); i++) {
            char c = ' ';
            if (i == -1) {
                c = '(';
            } else if (i == s.length()) {
                c = ')';
            } else {
                c = s.charAt(i);
            }
            
            if (Character.isDigit(c)) {
                sb.append(c);
            } else {
                if (sb.length() != 0) {
                    num.push(Integer.valueOf(sb.toString()));
                    sb = new StringBuilder();
                }
                
                if (c == '(' || c == '+' || c == '-') {
                    op.push(c);
                } else if (c == ')') {
                    while (op.peek() != '(') {
                        opR.push(op.pop());
                        numR.push(num.pop());
                    }
                    op.pop();
                    if (!opR.isEmpty()) {
                        numR.push(num.pop());
                        while (!opR.isEmpty()) {
                            char o = opR.pop();
                            int v1 = numR.pop();
                            int v2 = numR.pop();
                            if (o == '+') {
                                numR.push(v1 + v2);
                            } else if (o == '-') {
                                numR.push(v1 - v2);
                            }
                        }
                        num.push(numR.pop());
                    }
                }
            }
        }
        return num.pop();
    }
}
```
