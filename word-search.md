[Link](https://leetcode.com/problems/word-search/)

* 关注当前标， 一切非法不匹配，返回false

```java
public class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;
        boolean[][] visited = new boolean[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (find(word, board, 0, i, j, visited)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    private boolean find(String word, char[][] board, 
                         int pos, int row, int col,
                         boolean[][] visited) {
        if (pos == word.length()) {
            return true;
        }
        if (row < 0 || row >= board.length
                || col < 0 || col >= board[0].length
                || visited[row][col]
                || word.charAt(pos) != board[row][col]) {
            return false;
        }
        int[] rAdd = new int[]{0, 0, -1, 1};
        int[] cAdd = new int[]{-1, 1, 0, 0};
        visited[row][col] = true;
        for (int i = 0; i < 4; i++) {
            int rNext = row + rAdd[i];
            int cNext = col + cAdd[i];
            if (find(word, board, pos + 1, rNext, cNext, visited)) {
                return true;
            }
        }
        visited[row][col] = false;
        return false;
    }
}
```
