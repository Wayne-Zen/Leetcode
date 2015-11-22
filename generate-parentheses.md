[Link](https://leetcode.com/problems/generate-parentheses/)

＊ 比较左右括号个数。当左括号出现次数<n时，就可以放置新的左括号。当右括号出现次数小于左括号出现次数时，就可以放置新的右括号。

```java
public class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<String>();
        List<Character> now = new ArrayList<Character>();
        int lc = 0;
        int rc = 0;
        help(res, now, lc, rc, n);
        return res;
    }
    
    private void help(List<String> res, List<Character> now,
                      int lc, int rc, int n) {
        if (lc == n && rc == n) {
            char[] now_arr = new char[now.size()];
            for (int i = 0; i < now.size(); i++) {
                now_arr[i] = now.get(i);
            }
            res.add(String.valueOf(now_arr));
            return;
        }
        if (lc < n) {
            now.add('(');
            lc++;
            help(res, now, lc, rc, n);
            lc--;
            now.remove(now.size() - 1);
        }
        if (lc > rc) {
            now.add(')');
            rc++;
            help(res, now, lc, rc, n);
            rc--;
            now.remove(now.size() - 1);
        }
    }
}
```
