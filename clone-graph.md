[Link](https://leetcode.com/problems/clone-graph/)

```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null) {
            return null;
        }
        HashMap<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();
        Queue<UndirectedGraphNode> q = new LinkedList<UndirectedGraphNode>();
        q.offer(node);
        while (!q.isEmpty()) {
            UndirectedGraphNode now = q.poll();
            UndirectedGraphNode cp = new UndirectedGraphNode(now.label);
            map.put(now, cp);
            for (UndirectedGraphNode neighbor : now.neighbors) {
                if (map.containsKey(neighbor)) {
                    continue;
                }
                q.offer(neighbor);
            }
        }
        
        for (UndirectedGraphNode s : map.keySet()) {
            for (UndirectedGraphNode neighbor : s.neighbors) {
                map.get(s).neighbors.add(map.get(neighbor));
            }
        }
        return map.get(node);
    }
}
```
