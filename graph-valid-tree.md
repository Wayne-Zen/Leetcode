[Link](https://leetcode.com/problems/graph-valid-tree/)

```java
public class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (n == 0) {
            return false;
        }
        HashMap<Integer, HashSet<Integer>> graph = new HashMap<Integer, HashSet<Integer>>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
        }
        for (int i = 0; i < edges.length; i++) {
            int s = edges[i][0];
            int t = edges[i][1];
            graph.get(s).add(t);
            graph.get(t).add(s);
        }
        HashSet<Integer> visited = new HashSet<Integer>();
        Queue<Integer> q = new LinkedList<Integer>();
        visited.add(0);
        q.offer(0);
        while (!q.isEmpty()) {
            int s = q.poll();
            for (int t : graph.get(s)) {
                graph.get(t).remove(s);
                if (visited.contains(t)) {
                    return false;
                }
                q.offer(t);
                visited.add(t);
            }
            graph.remove(s);
        }
    
        return visited.size() == n;
    }
}
```

```java
public class Solution {
    class UF {
        int count;
        int[] parent;
        int[] rank;
        public UF(int n) {
            count = n;
            parent = new int[n];
            rank = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
                rank[i] = 1;
            }
        }
        public int find(int x) {
            while (x != parent[x]) {
                parent[x] = parent[parent[x]];
                x = parent[x];
            }
            return x;
        } 
        public boolean isConnected(int x, int y) {
            return find(x) == find(y);
        }
        public void union(int x, int y) {
            int rootX = find(x);
            int rootY = find(y);
            if (rootX == rootY) {
                return;
            }
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootX] = rootY;
                rank[rootY]++;
            }
            count--;
        }
    }
    public boolean validTree(int n, int[][] edges) {
        UF uf = new UF(n);
        for (int i = 0; i < edges.length; i++) {
            int n1 = edges[i][0];
            int n2 = edges[i][1];
            if (uf.isConnected(n1, n2)) {
                return false;
            } else {
                uf.union(n1, n2);
            }
        }
        return uf.count == 1;
    }
}
```
