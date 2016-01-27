[Link](https://leetcode.com/problems/minimum-height-trees/)

```java
public class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        HashMap<Integer, HashSet<Integer>> graph = new HashMap<Integer, HashSet<Integer>>();
        HashMap<Integer, Integer> degree = new HashMap<Integer, Integer>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
            degree.put(i, 0);
        }
        for (int i = 0; i < edges.length; i++) {
            int s = edges[i][0];
            int t = edges[i][1];
            graph.get(s).add(t);
            graph.get(t).add(s);
            degree.put(s, degree.get(s) + 1);
            degree.put(t, degree.get(t) + 1);
        }
        Queue<Integer> q = new LinkedList<Integer>();
        for (int i = 0; i < n; i++) {
            if (degree.get(i) == 1) {
                q.offer(i);
            }
        }
        while (graph.size() > 2) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int s = q.poll();
                int t = graph.get(s).iterator().next();
                graph.get(t).remove(s);
                graph.remove(s);
                degree.put(t, degree.get(t) - 1);
                degree.remove(s);
                if (degree.get(t) == 1) {
                    q.offer(t);
                }
            }
        }
        List<Integer> res = new ArrayList<Integer>();
        res.addAll(graph.keySet());
        return res;
    }
}
```
