[Link](https://leetcode.com/problems/minimum-height-trees/)

```java
public class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        List<Integer> res = new ArrayList<Integer>();
        if (n == 0) {
            return res;
        }
        if (n == 1) {
            res.add(0);
            return res;
        }
        HashMap<Integer, List<Integer>> graph = new HashMap<Integer, List<Integer>>();
        HashMap<Integer, Integer> degree = new HashMap<Integer, Integer>();
        for (int i = 0; i < edges.length; i++) {
            int n0 = edges[i][0];
            int n1 = edges[i][1];
            if (graph.containsKey(n0)) {
                graph.get(n0).add(n1);
            } else {
                List<Integer> neighbors = new ArrayList<Integer>();
                neighbors.add(n1);
                graph.put(n0, neighbors);
            }
            if (graph.containsKey(n1)) {
                graph.get(n1).add(n0);
            } else {
                List<Integer> neighbors = new ArrayList<Integer>();
                neighbors.add(n0);
                graph.put(n1, neighbors);
            }
            if (degree.containsKey(n0)) {
                degree.put(n0, degree.get(n0) + 1);
            } else {
                degree.put(n0, 1);
            }
            if (degree.containsKey(n1)) {
                degree.put(n1, degree.get(n1) + 1);
            } else {
                degree.put(n1, 1);
            }
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
                int t = graph.get(s).get(0);
                degree.put(s, degree.get(s) - 1);
                degree.put(t, degree.get(t) - 1);
                graph.remove(Integer.valueOf(s));
                graph.get(t).remove(Integer.valueOf(s));
                if (degree.get(t) == 1) {
                    q.offer(t);
                }
            }
        }
        res.addAll(q);
        return res;
    }
}
```
