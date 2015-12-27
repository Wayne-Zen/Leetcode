[Link](https://leetcode.com/problems/simplify-path/)


```java
public class Solution {
    public String simplifyPath(String path) {
        StringBuilder sb = new StringBuilder();
        LinkedList<String> list = new LinkedList<String>();
        char prev = '/';
        path = path + "/";
        for (int i = 0; i < path.length(); i++) {
            char c = path.charAt(i);
            if (c == '/') {
                if (prev != '/') {
                    String token = sb.toString();
                    sb = new StringBuilder();
                    if (token.equals(".")) {
                        // do nothing
                    } else if (token.equals("..")) {
                        if (!list.isEmpty()) {
                            list.removeLast();
                        }
                    } else {
                        list.addLast(token);
                    }
                }
            } else {
                sb.append(c);
            }
            prev = c;
        }
        if (list.size() == 0) {
            return "/";
        }
        sb = new StringBuilder();
        Iterator<String> iter = list.iterator();
        while (iter.hasNext()) {
            sb.append("/");
            sb.append(iter.next());
        }
        return sb.toString();
    }
}
```
