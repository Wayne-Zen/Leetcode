[Link](https://leetcode.com/problems/course-schedule-ii/)

```java
public class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        HashMap<Integer, List<Integer>> graph = new HashMap<Integer, List<Integer>>();
        HashMap<Integer, Integer> indegree = new HashMap<Integer, Integer>();
        for (int i = 0; i < prerequisites.length; i++) {
            int v1 = prerequisites[i][0]; // v1 ==> v2;
            int v2 = prerequisites[i][1];
            if (!graph.containsKey(v1)) {
                List<Integer> next = new ArrayList<Integer>();
                next.add(v2);
                graph.put(v1, next);
            } else {
                graph.get(v1).add(v2);
            }
            if (!indegree.containsKey(v2)) {
                indegree.put(v2, 1);
            } else {
                indegree.put(v2, indegree.get(v2) + 1);
            }
        }
        Queue<Integer> q = new LinkedList<Integer>();
        ArrayList<Integer> order = new ArrayList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (!indegree.containsKey(i)) {
                q.offer(i);
                order.add(i);
            }
        }
        while (!q.isEmpty()) {
            int s = q.poll();
            if (!graph.containsKey(s)) {
                continue;
            }
            for (int t : graph.get(s)) {
                // s ==> t
                indegree.put(t, indegree.get(t) - 1);
                if (indegree.get(t) == 0) {
                    q.offer(t);
                    order.add(t);
                }
            }
        }
        if (order.size() != numCourses) {
            return new int[]{};
        }
        Collections.reverse(order);
        int[] res = new int[order.size()];
        for (int i = 0; i < order.size(); i++) {
            res[i] = order.get(i);
        }
        return res;
    }
}
```
