[Link](https://leetcode.com/problems/game-of-life/)

```java
public class Solution {
    public void gameOfLife(int[][] board) {
        int[] r = {-1, -1, -1, 0, 0, 1, 1, 1};
        int[] c = {-1, 0, 1, -1, 1, -1, 0, 1};
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                int live = 0;
                for (int k = 0; k < 8; k++) {
                    int row = i + r[k];
                    int col = j + c[k];
                    if (row < 0 || row >= board.length
                            || col < 0 || col >= board[0].length) {
                        continue;
                    }
                    live += (board[row][col] & 1);
                }
                // 读取时需要屏蔽高位
                if ((board[i][j] & 1) == 0) {
                    if (live == 3) {
                        board[i][j] += 2;
                    }
                    continue;
                }
                if (live < 2) {
                    board[i][j] += 0;
                } else if (live == 2 || live == 3) {
                    board[i][j] += 2;
                } else if (live > 3) {
                    board[i][j] += 0;
                }
            }
        }
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                board[i][j] >>= 1;
            }
        }
    }
}
```
