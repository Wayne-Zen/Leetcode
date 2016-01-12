[Link](https://leetcode.com/problems/course-schedule/)

```java
public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        HashMap<Integer, List<Integer>> graph = new HashMap<Integer, List<Integer>>();
        HashMap<Integer, Integer> indegree = new HashMap<Integer, Integer>();
        for (int i = 0; i < numCourses; i++) {
            graph.put(i, new ArrayList<Integer>());
            indegree.put(i, 0);
        }
        for (int i = 0; i < prerequisites.length; i++) {
            int v1 = prerequisites[i][0]; // v1 ===> v2
            int v2 = prerequisites[i][1];
            graph.get(v1).add(v2);
            indegree.put(v2, indegree.get(v2) + 1);
        }

        Queue<Integer> q = new LinkedList<Integer>();
        int cnt = 0;
        for (int i = 0; i < numCourses; i++) {
            if (indegree.get(i) == 0) {
                q.offer(i);
                cnt++;
            }
        }
        while (!q.isEmpty()) {
            int s = q.poll();
            for (int t : graph.get(s)) {
                // s ==> t
                indegree.put(t, indegree.get(t) - 1);
                if (indegree.get(t) == 0) {
                    q.offer(t);
                    cnt++;
                }
            }
        }
        return cnt == numCourses;
    }
}
```
