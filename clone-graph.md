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
        HashMap<UndirectedGraphNode, UndirectedGraphNode> map = 
                new HashMap<UndirectedGraphNode, UndirectedGraphNode>();
        Queue<UndirectedGraphNode> q = new LinkedList<UndirectedGraphNode>();
        q.offer(node);
        map.put(node, new UndirectedGraphNode(node.label));
        while (!q.isEmpty()) {
            UndirectedGraphNode n = q.poll();
            for (UndirectedGraphNode neighbor : n.neighbors) {
                if (map.containsKey(neighbor)) {
                    continue;
                }
                q.offer(neighbor);
                map.put(neighbor, new UndirectedGraphNode(neighbor.label));
            }
        }
        
        for (UndirectedGraphNode n : map.keySet()) {
            for (UndirectedGraphNode neighbor : n.neighbors) {
                map.get(n).neighbors.add(map.get(neighbor));
            }
        }
        
        return map.get(node);
    }
}
```
