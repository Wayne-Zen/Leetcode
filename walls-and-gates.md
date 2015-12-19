[Link](https://leetcode.com/problems/walls-and-gates/)

```java
public class Solution {
    public void wallsAndGates(int[][] rooms) {
        if (rooms == null || rooms.length == 0 || rooms[0].length == 0) {
            return;
        }
        int m = rooms.length;
        int n = rooms[0].length;
        Queue<Integer> q = new LinkedList<Integer>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (rooms[i][j] == 0) {
                    q.offer(i * n + j);
                }
            }
        }
        int[] rAdd = new int[]{1, -1, 0, 0};
        int[] cAdd = new int[]{0, 0, 1, -1};
        while (!q.isEmpty()) {
            int loc = q.poll();
            int row = loc / n;
            int col = loc % n;
            for (int i = 0; i < 4; i++) {
                int r = row + rAdd[i];
                int c = col + cAdd[i];
                if (r < 0 || r >= m || c < 0 || c >= n 
                        || rooms[r][c] == -1 || rooms[r][c] != Integer.MAX_VALUE) {
                    continue;
                }
                rooms[r][c] = rooms[row][col] + 1;
                q.add(r * n + c);
            }
        }
    }
}
```
