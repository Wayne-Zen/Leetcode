[Link](https://leetcode.com/problems/palindrome-partitioning/)


```java
public class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<List<String>>();
        List<String> now = new ArrayList<String>(); // bar location
        help(res, now, s, 0);
        return res;
    }
    private void help(List<List<String>> res,
                      List<String> now,
                      String s, int pos) {
        if (pos == s.length()) {
            res.add(new ArrayList<String>(now));
            return;
        }
        for (int i = pos; i < s.length(); i++) {
            String substr = s.substring(pos, i + 1);
            if (!isPalin(substr)) {
                continue;
            }
            now.add(substr);
            help(res, now, s, i + 1);
            now.remove(now.size() - 1);
        }
    }
    private boolean isPalin(String s) {
        int head = 0; 
        int tail = s.length() - 1;
        while (head < tail) {
            if (s.charAt(head) != s.charAt(tail)) {
                return false;
            } else {
                head++;
                tail--;
            }
        }
        return true;
    }
}
```
