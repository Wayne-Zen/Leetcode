[Link](https://leetcode.com/problems/remove-invalid-parentheses/)

```java
public class Solution {
    public List<String> removeInvalidParentheses(String s) {
        Queue<String> q = new LinkedList<String>(); // store invalid only
        List<String> res = new ArrayList<String>();
        if (getDist(s) == 0) {
            res.add(s);
        } else {
            q.offer(s);
        }
        while (res.size() == 0) {
            int size = q.size();
            HashSet<String> visited = new HashSet<String>();
            for (int i = 0; i < size; i++) {
                String now = q.poll();
                for (int k = 0; k < now.length(); k++) {
                    if (now.charAt(k) != '(' && now.charAt(k) != ')') {
                        continue;
                    }
                    String next = now.substring(0, k) + now.substring(k + 1);
                    if (visited.contains(next)) {
                        continue;
                    } else {
                        visited.add(next);
                    }
                    if (getDist(next) == 0) {
                        res.add(next);
                    } else {
                        q.offer(next);
                    }
                }
            }
        }
        return res;
    }
    private int getDist(String s) {
        int a = 0;
        int b = 0;
        for (char c : s.toCharArray()) {
            if (c == '(') {
                a++;
            } else if (c == ')') {
                a--;
            }
            b += a < 0 ? -a : 0;
            a = Math.max(0, a);
        }
        return a + b;
    }
}
```
```java
// HashSet 纪录结果
// 除了rmL, rmR, 还要reverse, 因为一旦出现多余的')', 就没有办法挽回了
public class Solution {
    public List<String> removeInvalidParentheses(String s) {
        HashSet<String> res = new HashSet<String>();
        int aCnt = 0, bCnt = 0;
        for(char c : s.toCharArray()) {
            if(c == '(') {
                aCnt++;
            } else if(c == ')') {
                aCnt--;
            }
            bCnt += aCnt < 0 ? 1 : 0;
            aCnt = Math.max(0, aCnt);
        }
        DFS(res, s, 0, aCnt, bCnt, "", 0);
        return new ArrayList<String>(res);  
    }
    public void DFS(HashSet<String> res, String s, int pos, int rmL, int rmR, String now, int reverse) {
        if (rmL < 0 || rmR < 0 || reverse > 0) {
            return;
        }
        if (pos == s.length()) {
            if (rmL == 0 && rmR == 0 && reverse == 0) {
                res.add(now);
            }
            return;
        }
        char c = s.charAt(pos);
        if(c == '(') {
            DFS(res, s, pos + 1, rmL - 1, rmR, now, reverse);
            DFS(res, s, pos + 1, rmL, rmR, now + c, reverse - 1); 
    
        } else if(c == ')') {
            DFS(res, s, pos + 1, rmL, rmR - 1, now, reverse);
            DFS(res, s, pos + 1, rmL, rmR, now + c, reverse + 1);
    
        } else {
            DFS(res, s, pos + 1, rmL, rmR, now + c, reverse); // add c
        }
    }
}
```
