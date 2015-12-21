[Link](https://leetcode.com/problems/sudoku-solver/)

```java
public class Solution {
    public void solveSudoku(char[][] board) {
        List<Integer> locs = new ArrayList<Integer>();
        List<Character> res = new ArrayList<Character>();
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') {
                    locs.add(i * 9 + j);
                }
            }
        }
        if (!help(board, locs, res)) {
            return;
        }
        for (int i = 0; i < res.size(); i++) {
            int loc = locs.get(i);
            board[loc / 9][loc % 9] = res.get(i);
        }
    }
    private boolean help(char[][] board, List<Integer> locs, List<Character> res) {
        if (res.size() == locs.size()) {
            return true;
        }
        int loc = locs.get(res.size());
        int row = loc / 9;
        int col = loc % 9;
        List<Character> cand = getCand(board, row, col);
        for (char c : cand) {
            board[row][col] = c;
            res.add(c);
            if (help(board, locs, res)) {
                return true;
            }
            board[row][col] = '.';
            res.remove(res.size() - 1);
        }
        return false;
    }
    private List<Character> getCand(char[][] board, int row, int col) {
        boolean[] show = new boolean[9];
        int rBase = (row / 3) * 3;
        int cBase = (col / 3) * 3;
        for (int k = 0; k < 9; k++) {
            if (board[row][k] != '.') {
                show[board[row][k] - '1'] = true;
            }
            if (board[k][col] != '.') {
                show[board[k][col] - '1'] = true;
            }
            if (board[rBase + k / 3][cBase + k % 3] != '.') {
                show[board[rBase + k / 3][cBase + k % 3] - '1'] = true;
            }
        }
        List<Character> res = new ArrayList<Character>();
        for (int i = 0; i < 9; i++) {
            if (!show[i]) {
                res.add((char)('1' + i));
            }
        }
        return res;
    }
}
```
