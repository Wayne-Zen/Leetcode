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
    
    private ArrayList<Character> getChoices(char[][] board, Cell cell) {
        int row = cell.row;
        int col = cell.col;
        ArrayList<Character> ret = new ArrayList<Character>();
        for (char c = '1'; c <= '9'; c++) {
            ret.add(c);
        }
        for (int i = 0; i < 9; i++) {
            ret.remove(Character.valueOf(board[row][i]));
        }
        for (int i = 0; i < 9; i++) {
            ret.remove(Character.valueOf(board[i][col]));
        }
        int rBase = row - row % 3;
        int cBase = col - col % 3;
        for (int i = 0; i < 9; i++) {
            ret.remove(Character.valueOf(board[rBase + i / 3][cBase + i % 3]));
        }
        return ret;
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
        ArrayList<Character> choices = getChoices(board, c);
        for (int i = 0; i < choices.size(); i++) {
            char choice = choices.get(i);
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
