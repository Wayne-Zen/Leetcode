[Link](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)

```java
public class Solution {
    class UF {
        int[] parent;
        int[] rank;
        int count;
        public UF(int N) {
            count = N;
            parent = new int[N];
            rank = new int[N];
            for (int i = 0; i < N; i++) {
                parent[i] = i;
                rank[i] = 1;
            }
        }
        public int find(int x) {
            while (parent[x] != x) {
                parent[x] = parent[parent[x]];
                x = parent[x];
            }
            return x;
        }
        public void union(int x, int y) {
            if (find(x) == find(y)) {
                return;
            }
            int rootX = find(x);
            int rootY = find(y);
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
            count--;
        }
    }
    public int countComponents(int n, int[][] edges) {
        UF uf = new UF(n);
        for (int i = 0; i < edges.length; i++) {
            int x = edges[i][0];
            int y = edges[i][1];
            uf.union(x, y);
        }
        return uf.count;
    }
}
```
