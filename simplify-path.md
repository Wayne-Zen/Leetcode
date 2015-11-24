[Link](https://leetcode.com/problems/simplify-path/)


```java
public class Solution {
    public String simplifyPath(String path) {
        Stack<String> stack = new Stack<String>();
        StringBuilder sub = new StringBuilder();
        for (int i = 0; i < path.length() + 1; i++) {
            char c = '/';
            if (i != path.length()) {
                c = path.charAt(i);
            }
            if (c == '/' && sub.length() != 0) {
                String s = sub.toString();
                sub = new StringBuilder();
                if (s.equals(".")) {
                    // do nothing
                } else if (s.equals("..")) {
                    if (!stack.isEmpty()) {
                        stack.pop();
                    }
                } else {
                    stack.push(s);
                }
                continue;
            } 
            if (c != '/') {
                sub.append(c);
            }
        }
        if (stack.isEmpty()) {
            return "/";
        }
        StringBuilder res = new StringBuilder();
        Stack<String> rev = new Stack<String>();
        while (!stack.isEmpty()) {
            rev.push(stack.pop());
        }
        while (!rev.isEmpty()) {
            res.append('/');
            res.append(rev.pop());
        }
        return res.toString();
    }
}
```
