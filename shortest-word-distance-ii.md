[Link](https://leetcode.com/problems/shortest-word-distance-ii/)

```java
public class WordDistance {
    HashMap<String, List<Integer>> map = new HashMap<String, List<Integer>>();
    public WordDistance(String[] words) {
        for (int i = 0; i < words.length; i++) {
            String w = words[i];
            if (map.containsKey(w)) {
                map.get(w).add(i);
            } else {
                List<Integer> locs = new ArrayList<Integer>();
                locs.add(i);
                map.put(w, locs);
            }
        }
    }

    public int shortest(String word1, String word2) {
        List<Integer> l1 = map.get(word1);
        List<Integer> l2 = map.get(word2);
        int min = Integer.MAX_VALUE;
        for (int i1 : l1) {
            for (int i2 : l2) {
                min = Math.min(min, Math.abs(i1 - i2));
            }
        }
        return min;
    }
}

// Your WordDistance object will be instantiated and called as such:
// WordDistance wordDistance = new WordDistance(words);
// wordDistance.shortest("word1", "word2");
// wordDistance.shortest("anotherWord1", "anotherWord2");
```
