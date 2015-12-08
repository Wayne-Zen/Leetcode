[Link](https://leetcode.com/problems/remove-invalid-parentheses/)

```java
public class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> res = new ArrayList<String>();
        Queue<String> q = new LinkedList<String>(); // queue 里全是非法的
        int maxMis = getMisMatch(s);
        if (maxMis == 0) {
            res.add(s);
        } else {
            q.offer(s);
        }
        for (int level = maxMis; level > 0; level--) {
            HashSet<String> visited = new HashSet<String>();
            int size = q.size();
            for (int i = 0; i < size; i++) {
                String now = q.poll();
                for (int k = 0; k < now.length(); k++) {
                    if (now.charAt(k) != '(' && now.charAt(k) != ')') {
                        continue;
                    }
                    String del = now.substring(0, k) + now.substring(k + 1, now.length());
                    if (!visited.contains(del) && getMisMatch(del) == level - 1) {
                        q.offer(del);
                        visited.add(del);
                        if (level == 1) {
                            res.add(del);
                        }
                    }
                }
            }
        }
        return res;
    }
    private int getMisMatch(String s) {
        int a = 0;
        int b = 0;
        for (char c : s.toCharArray()) {
            if (c == '(') {
                a++;
            } else if (c == ')') {
                a--;
            }
            b += a < 0 ? 1 : 0;
            a = Math.max(0, a);
        }
        return a + b;
    }
}
```
