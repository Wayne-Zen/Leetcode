[Link](https://leetcode.com/problems/sudoku-solver/)

```java
public class Solution {
    private class Cell {
        int row;
        int col;
        public Cell(int row, int col) {
            this.row = row;
            this.col = col;
        }
    }
    
    public void solveSudoku(char[][] board) {
        ArrayList<Cell> cells = new ArrayList<Cell>();
        ArrayList<Character> now = new ArrayList<Character>();
        ArrayList<ArrayList<Character>> ans = new ArrayList<ArrayList<Character>>();
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') {
                    cells.add(new Cell(i, j));
                }
            }
        }
        help(ans, now, cells, 0, board);
        fill(board, ans.get(0), cells);
    }
    
    private void fill(char[][] board, ArrayList<Character> ans,
                      ArrayList<Cell> cells) {
        for (int i = 0; i < ans.size(); i++) {
            Cell c = cells.get(i);
            board[c.row][c.col] = ans.get(i);
        }        
    }
    
    private boolean[] getChoices(char[][] board, Cell cell) {
        int row = cell.row;
        int col = cell.col;
        boolean[] exist = new boolean[9];
        for (int i = 0; i < 9; i++) {
            char c = board[row][i];
            if (c != '.') {
                exist[c - '1'] = true;
            }
        }
        for (int i = 0; i < 9; i++) {
            char c = board[i][col];
            if (c != '.') {
                exist[c - '1'] = true;
            }
        }
        int rBase = row - row % 3;
        int cBase = col - col % 3;
        for (int i = 0; i < 9; i++) {
            char c = board[rBase + i / 3][cBase + i % 3];
            if (c != '.') {
                exist[c - '1'] = true;
            }
        }
        return exist;
    }
    
    private void help(ArrayList<ArrayList<Character>> ans,
                      ArrayList<Character> now,
                      ArrayList<Cell> cells,
                      int pos, char[][] board) {
        if (now.size() == cells.size()) {
            ans.add(new ArrayList<Character>(now));
            return;
        }
        Cell c = cells.get(pos);
        boolean[] choices = getChoices(board, c);
        for (int i = 0; i < 9; i++) {
            if (choices[i]) {
                continue;
            }
            char choice = (char)('1' + i);
            now.add(choice);
            board[c.row][c.col] = choice;
            help(ans, now, cells, pos + 1, board);
            if (ans.size() != 0) {
                break;
            }
            now.remove(now.size() - 1);
            board[c.row][c.col] = '.';
        }
    }
}
```
