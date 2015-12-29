[Link](https://leetcode.com/problems/basic-calculator/)

```java
public class Solution {
    public int calculate(String s) {
        s = "(" + s + ")";
        Stack<Integer> vs = new Stack<Integer>();
        Stack<Character> os = new Stack<Character>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                int val = 0;
                while (Character.isDigit(c)) {
                    val = val * 10 + c - '0';
                    c = s.charAt(++i);
                }
                vs.push(val);
                i--;
            } else if (c == '(' || c == '+' || c == '-') {
                os.push(c);
            } else if (c == ')') {
                int val = 0;
                while (os.peek() != '(') {
                    val += (os.pop() == '+' ? 1 : -1) * vs.pop();
                }
                val += vs.pop();
                os.pop(); // '('
                vs.push(val);
            }
        }
        return vs.pop();
    }
}
```
