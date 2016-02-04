[Link](https://leetcode.com/problems/reconstruct-itinerary/)

```java
public class Solution {
    public List<String> findItinerary(String[][] tickets) {
        HashMap<String, ArrayList<String>> graph = new HashMap<String, ArrayList<String>>();
        for (int i = 0; i < tickets.length; i++) {
            String from = tickets[i][0];
            String to = tickets[i][1];
            if (!graph.containsKey(from)) {
                graph.put(from, new ArrayList<String>());
            }
            if (!graph.containsKey(to)) {
                graph.put(to, new ArrayList<String>());
            }
            graph.get(from).add(to);
        }
        List<String> res = new ArrayList<String>();
        res.add("JFK");
        help(res, "JFK", tickets.length, graph);
        return res;
    }
    private boolean help(List<String> res, String now, int remain,
                      HashMap<String, ArrayList<String>> graph) {
        if (remain == 0) {
            return true;
        }
        List<String> nexts = new ArrayList<String>();
        nexts.addAll(graph.get(now));
        Collections.sort(nexts);
        for (String next : nexts) {
            graph.get(now).remove(next);
            res.add(next);
            if (help(res, next, remain - 1, graph)) {
                return true;
            }
            graph.get(now).add(next);
            res.remove(res.size() - 1);
        }
        return false;
    }
}
```
