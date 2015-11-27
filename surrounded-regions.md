[Link](https://leetcode.com/problems/surrounded-regions/)

```java
public class Solution {
	public void solve(char[][] board) {
		if (board == null || board.length == 0)
			return;
 
		int m = board.length;
		int n = board[0].length;
 
		// merge O's on left & right boarder
		for (int i = 0; i < m; i++) {
			if (board[i][0] == 'O') {
				bfs(board, i, 0);
			}
 
			if (board[i][n - 1] == 'O') {
				bfs(board, i, n - 1);
			}
		}
 
		// merge O's on top & bottom boarder
		for (int j = 0; j < n; j++) {
			if (board[0][j] == 'O') {
				bfs(board, 0, j);
			}
 
			if (board[m - 1][j] == 'O') {
				bfs(board, m - 1, j);
			}
		}
 
		// process the board
		for (int i = 0; i < m; i++) {
			for (int j = 0; j < n; j++) {
				if (board[i][j] == 'O') {
					board[i][j] = 'X';
				} else if (board[i][j] == '#') {
					board[i][j] = 'O';
				}
			}
		}
	}
 
    private void bfs(char[][] board, int r, int c) {
        board[r][c] = '#';
        int N = board[0].length;
        int[] rNext = new int[]{1, -1, 0, 0};
        int[] cNext = new int[]{0, 0, 1, -1};
        LinkedList<Integer> queue = new LinkedList<Integer>();
        queue.add(r * N + c);
        while (!queue.isEmpty()) {
            int loc = queue.poll();
            int row = loc / N;
            int col = loc % N;
            for (int k = 0; k < 4; k++) {
                int newRow = row + rNext[k];
                int newCol = col + cNext[k];
                if (newRow > 0 && newRow < board.length 
                        && newCol > 0 && newCol < board[0].length
                        && board[newRow][newCol] == 'O') {
                    queue.offer(newRow * N + newCol);
                    board[newRow][newCol] = '#';
                }
            }
        }
    }
}
```
