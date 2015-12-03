[Link](https://leetcode.com/problems/alien-dictionary/)

```java
public class Solution {
    public String alienOrder(String[] words) {
        HashMap<Character, HashSet<Character>> graph = new HashMap<Character, HashSet<Character>>();
        HashMap<Character, Integer> degree = new HashMap<Character, Integer>();
        HashSet<Character> alphabet = new HashSet<Character>();
        for (String word : words) {
            for (char c : word.toCharArray()) {
                alphabet.add(c);
            }
        }
        // build graph
        for (int i = 1; i < words.length; i++) {
            String w1 = words[i - 1];
            String w2 = words[i];
            for (int j = 0; j < Math.min(w1.length(), w2.length()); j++) {
                if (w1.charAt(j) != w2.charAt(j)) {
                    char s = w1.charAt(j);
                    char t = w2.charAt(j);
                    boolean dup = false;
                    if (graph.containsKey(s)) {
                        if (!graph.get(s).contains(t)) {
                            graph.get(s).add(t);
                        } else {
                            dup = true;
                        }
                    } else {
                        HashSet<Character> neighbor = new HashSet<Character>();
                        neighbor.add(t);
                        graph.put(s, neighbor);
                    }
                    if (!dup) {
                        if (degree.containsKey(t)) {
                            degree.put(t, degree.get(t) + 1);
                        } else {
                            degree.put(t, 1);
                        }
                    }
                    break;
                }
            }
        }
        
        // sort
        List<Character> order = new ArrayList<Character>();
        Queue<Character> q = new LinkedList<Character>();
        for (char c = 'a'; c <= 'z'; c++) {
            if (alphabet.contains(c) && !degree.containsKey(c)) {
                q.offer(c);
                order.add(c);
            }
        }
        while (!q.isEmpty()) {
            char s = q.poll();
            if (!graph.containsKey(s)) {
                continue;
            }
            for (char t : graph.get(s)) {
                degree.put(t, degree.get(t) - 1);
                if (degree.get(t) == 0) {
                    q.offer(t);
                    order.add(t);
                }
            }
        }
        if (order.size() != alphabet.size()) {
            return "";
        }
        StringBuilder sb = new StringBuilder();
        for (char c : order) {
            sb.append(c);
        }
        //System.out.println(sb);
        return sb.toString();
    }
}
```
