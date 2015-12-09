[Link](https://leetcode.com/problems/n-queens-ii/)

```java
public class Solution {
    public int totalNQueens(int n) {
        int[] cnt = new int[1];
        List<Integer> now = new ArrayList<Integer>();
        boolean[] visited = new boolean[n];
        help(now, n, visited, cnt);
        return cnt[0];
    }
    private void help(List<Integer> now, int n, boolean[] visited, int[] cnt) {
        if (now.size() == n) {
            cnt[0]++;
            return;
        }
        for (int i = 0; i < n; i++) {
            if (visited[i] || !diag(now, i)) {
                continue;
            }
            now.add(i);
            visited[i] = true;
            help(now, n, visited, cnt);
            now.remove(now.size() - 1);
            visited[i] = false;
        }
    }
    private boolean diag(List<Integer> now, int index) {
        for (int i = 0; i < now.size(); i++) {
            int row1 = i;
            int col1 = now.get(i);
            int row2 = now.size();
            int col2 = index;
            if (row1 + col1 == row2 + col2 || row1 - col1 == row2 - col2) {
                return false;
            }
        }
        return true;
    }
}
```
