[Link](https://leetcode.com/problems/alien-dictionary/)

```java
public class Solution {
    public String alienOrder(String[] words) {
        HashSet<Character> alphabet = new HashSet<Character>();
        for (String word : words) {
            for (char c : word.toCharArray()) {
                alphabet.add(c);
            }
        }
        HashMap<Character, HashSet<Character>> graph = new HashMap<Character, HashSet<Character>>();
        HashMap<Character, Integer> degree = new HashMap<Character, Integer>();
        for (char c : alphabet) {
            graph.put(c, new HashSet<Character>());
            degree.put(c, 0);
        }
        // build graph, 每个相邻对只能确定一个有向边
        for (int i = 1; i < words.length; i++) {
            String w1 = words[i - 1];
            String w2 = words[i];
            for (int j = 0; j < Math.min(w1.length(), w2.length()); j++) {
                char s = w1.charAt(j);
                char t = w2.charAt(j);
                if (s == t) {
                    continue;
                }
                if (graph.get(s).contains(t)) {
                    continue;
                }
                graph.get(s).add(t);
                degree.put(t, degree.get(t) + 1);
                break;
            }
        }

        // sort
        StringBuilder res = new StringBuilder();
        Queue<Character> q = new LinkedList<Character>();
        for (char c : alphabet) {
            if (degree.get(c) == 0) {
                q.offer(c);
                res.append(c);
            }
        }
        while (!q.isEmpty()) {
            char s = q.poll();
            for (char t : graph.get(s)) {
                degree.put(t, degree.get(t) - 1);
                if (degree.get(t) == 0) {
                    q.offer(t);
                    res.append(t);
                }
            }
            graph.remove(s);
        }
        if (res.length() != alphabet.size()) {
            return "";
        }
        System.out.println(res);
        return res.toString();
    }
}
```
