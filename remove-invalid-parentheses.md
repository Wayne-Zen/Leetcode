[Link](https://leetcode.com/problems/remove-invalid-parentheses/)

```java
public class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> res = new ArrayList<String>();
        Queue<String> q = new LinkedList<String>();
        HashSet<String> visited = new HashSet<String>();
        q.offer(s);
        visited.add(s);
        int minMis = s.length();
        boolean find = false;
        while (!q.isEmpty()) {
            String now = q.poll();
            minMis = Math.min(minMis, check(now));
            if (minMis == 0) {
                find = true;
                res.add(now);
            }
            // if find a match, check the rest of queue, any more match
            // no more adding
            if (!find) {
                for (int i = 0; i < now.length(); i++) {
                    if (now.charAt(i) != '(' && now.charAt(i) != ')') {
                        continue;
                    }
                    String newStr = now.substring(0, i) + now.substring(i + 1);
                    //若得到的新字符串的失配括号比原字符串少，则继续搜索；否则剪枝。
                    if (!visited.contains(newStr) && check(newStr) < minMis) {
                        visited.add(newStr);
                        q.offer(newStr);
                    }
                }
            }
        }
        return res;
    }
    private int check(String s) {
        int a = 0;
        int b = 0;
        for (int i = 0; i < s.length(); i++) { // notice ")("
            if (s.charAt(i) == ')') {
                a--;
            }
            if (s.charAt(i) == '(') {
                a++;
            }
            b += a < 0 ? 1 : 0;
            a = Math.max(a, 0);
        }
        return a + b;
    }
}
```
