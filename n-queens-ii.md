[Link](https://leetcode.com/problems/n-queens-ii/)

```java
public class Solution {
    private int cnt = 0;
    public int totalNQueens(int n) {
        List<Integer> now = new ArrayList<Integer>();
        help(now, n);
        return cnt;
    }
    private void help(List<Integer> now, int n) {
        if (now.size() == n) {
            cnt++;
            return;
        }
        for (int i = 0; i < n; i++) {
            if (!valid(now, i)) {
                continue;
            }
            now.add(i);
            help(now, n);
            now.remove(now.size() - 1);
        }
    }
    private boolean valid(List<Integer> now, int index) {
        for (int i = 0; i < now.size(); i++) {
            int row1 = i;
            int col1 = now.get(i);
            int row2 = now.size();
            int col2 = index;
            if (now.get(i) == index 
                || Math.abs(row1 - row2) == Math.abs(col1 - col2)) {
                return false;
            }
        }
        return true;
    }
}
```
