[Link](https://leetcode.com/problems/word-search/)

```java
public class Solution {
    public boolean exist(char[][] board, String word) {
        if (word.length() == 0) {
            return true;
        }
        int m = board.length;
        int n = board[0].length;
        boolean[][] visited = new boolean[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] != word.charAt(0)) {
                    continue;
                }
                visited[i][j] = true;
                if (help(board, i, j, word, 0, visited)) {
                    return true;
                }
                visited[i][j] = false;
            }
        }
        return false;
    }
    private boolean help(char[][] board, int row, int col, String word, int pos, boolean[][] visited) {
        if (pos == word.length() - 1) {
            return true;
        }
        int[] rAdd = {1, -1, 0, 0};
        int[] cAdd = {0, 0, 1, -1};
        for (int i = 0; i < 4; i++) {
            int r = row + rAdd[i];
            int c = col + cAdd[i];
            if (r < 0 || r >= board.length || c < 0 || c >= board[0].length || board[r][c] != word.charAt(pos + 1) || visited[r][c]) {
                continue;
            }
            visited[r][c] = true;
            if (help(board, r, c, word, pos + 1, visited)) {
                return true;
            }
            visited[r][c] = false;
        }
        return false;
    }
}
```
