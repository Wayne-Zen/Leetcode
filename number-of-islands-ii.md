[Link](https://leetcode.com/problems/number-of-islands-ii/)

```java
public class Solution {
    class UF {
        private int[] parent;
        private int[] rank;
        int count;  //number of components
    
        public UF(int N) {
            if (N < 0) {
                throw new IllegalArgumentException();
            }
            parent = new int[N];
            rank = new int[N];
            count = N;
            for (int i = 0; i < N; i++) {
                parent[i] = i;
                rank[i] = 0; 
            }
        }
    
        public int findRoot(int p) {
            if (p < 0 || p >= parent.length) {
                throw new IndexOutOfBoundsException();
            }
            // root's parent is its self
            while (p != parent[p]) {
                parent[p] = parent[parent[p]];    // path compression
                p = parent[p];
            } 
            return p;
        }
    
        public boolean connected(int x, int y) {
            return findRoot(x) == findRoot(y);
        }
    
        public void union(int x, int y) {
            int rootX = findRoot(x);
            int rootY = findRoot(y);
            if (rootX == rootY) {
                return;
            }
    
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY; // x become child of y
            } else if (rank[rootY] < rank[rootX]) {
                parent[rootY] = rootX; // y become child of x
            } else { // equal size, rank + 1
                parent[rootX] = rootY;
                rank[rootY]++;
            }
            count--;
        }
    }
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        List<Integer> res = new ArrayList<Integer>();
        int[][] matrix = new int[m][n];
        UF uf = new UF(m * n);
        int cnt = 0;
        for (int i = 0; i < positions.length; i++) {
            cnt++;
            int r = positions[i][0];
            int c = positions[i][1];
            matrix[r][c] = 1;
            
            int[] rAdd = new int[]{1, -1, 0, 0};
            int[] cAdd = new int[]{0, 0, 1, -1};
            for (int k = 0; k < 4; k++) {
                int row = r + rAdd[k];
                int col = c + cAdd[k];
                if (row < 0 || row >= m || col < 0 || col >= n
                        || matrix[row][col] == 0) {
                    continue;
                }
                if (!uf.connected(r * n + c, row * n + col)) {
                    cnt--;
                    uf.union(r * n + c, row * n + col);
                } 
            }
            res.add(cnt);
        }
        return res;
    }
}
```
