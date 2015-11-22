[Link](https://leetcode.com/problems/valid-parentheses/)

* 正向括号push，反向检查
* 确保pop无异常
* 确保结束时，栈为空

```java
public class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
                continue; 
            }
            // 坑：保证可以pop
            if (stack.isEmpty()) {
                return false;
            }
            if (c == ']') {
                if (stack.peek() != '[') {
                    return false;
                } else {
                    stack.pop();
                }
            }
            if (c == ')') {
                if (stack.peek() != '(') {
                    return false;
                } else {
                    stack.pop();
                }
            }
            if (c == '}') {
                if (stack.peek() != '{') {
                    return false;
                } else {
                    stack.pop();
                }
            }
        }
        // 坑：确保结束时，栈为空
        if (!stack.isEmpty()) {
            return false;
        }
        return true;
    }
    
}
```
