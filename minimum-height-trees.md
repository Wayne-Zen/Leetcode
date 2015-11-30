[Link](https://leetcode.com/problems/minimum-height-trees/)

```java
public class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        HashMap<Integer, List<Integer>> graph = new HashMap<Integer, List<Integer>>();
        for (int i = 0; i < edges.length; i++) {
            int s = edges[i][0];
            int t = edges[i][1];
            if (graph.containsKey(s)) {
                graph.get(s).add(t);
            } else {
                List<Integer> neighbor = new ArrayList<Integer>();
                neighbor.add(t);
                graph.put(s, neighbor);
            }
            if (graph.containsKey(t)) {
                graph.get(t).add(s);
            } else {
                List<Integer> neighbor = new ArrayList<Integer>();
                neighbor.add(s);
                graph.put(t, neighbor);
            }
        }
        ArrayList<Integer> leaves = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            if (graph.containsKey(i) && graph.get(i).size() == 1) {
                leaves.add(i);
            }
        }
        while (n > 2) {
            n -= leaves.size();
            ArrayList<Integer> newLeaves = new ArrayList<Integer>();
            for (int i = 0; i < leaves.size(); i++) {
                int leaf = leaves.get(i);
                int s = graph.get(leaf).get(0);
                graph.get(s).remove(Integer.valueOf(leaf));
                if (graph.get(s).size() == 1) {
                    newLeaves.add(s);
                }
            }
            leaves = newLeaves;
        }
        if (leaves.size() == 0) {
            leaves.add(0);
        }
        return leaves;
    }
}
```
