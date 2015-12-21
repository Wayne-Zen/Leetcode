[Link](https://leetcode.com/problems/valid-sudoku/)



```java
public class Solution {
    public boolean isValidSudoku(char[][] board) {
        boolean[] visited = new boolean[9];
        //row
        for (int i = 0; i < 9; i++) {
            Arrays.fill(visited, false);
            for (int j = 0; j < 9; j++) {
                if (!check(visited, board[i][j])) {
                    return false;
                }
            }
        }
        // col
        for (int j = 0; j < 9; j++) {
            Arrays.fill(visited, false);
            for (int i = 0; i < 9; i++) {
                if (!check(visited, board[i][j])) {
                    return false;
                }
            }
        }
        // block
        for (int i = 0; i < 9; i += 3){
            for (int j = 0; j < 9; j += 3){
                Arrays.fill(visited, false);
                for (int k = 0; k < 9; k++){
                    if (!check(visited, board[i + k / 3][j + k % 3])) {
                        return false;
                    }
                }
            }
        }
        return true;
    }
    
    private boolean check(boolean[] visited, char c) {
        if (c == '.') {
            return true;
        }
        int num = c - '1';
        if (num < 0 || num >= 9 || visited[num]) {
            return false;
        }
        visited[num] = true;
        return true;
    }
}
```
