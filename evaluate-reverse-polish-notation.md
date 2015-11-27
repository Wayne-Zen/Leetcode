[Link](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

```java
public class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<Integer>();
        for (String t : tokens) {
            if (t.equals("+")) {
                int val = stack.pop() + stack.pop();
                stack.push(val);
            } else if (t.equals("*")) {
                int val = stack.pop() * stack.pop();
                stack.push(val);
            } else if (t.equals("-")) {
                int v1 = stack.pop();
                int v2 = stack.pop();
                stack.push(v2 - v1);
            } else if (t.equals("/")) {
                int v1 = stack.pop();
                int v2 = stack.pop();
                stack.push(v2 / v1);
            } else {
                stack.push(new Integer(t));
            }
        }
        return stack.pop();
    }
}
```
