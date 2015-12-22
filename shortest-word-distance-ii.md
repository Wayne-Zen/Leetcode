[Link](https://leetcode.com/problems/shortest-word-distance-ii/)

```java
public class WordDistance {
    // str -> indexes
    HashMap<String, List<Integer>> map = new HashMap<String, List<Integer>>();
    public WordDistance(String[] words) {
        for (int i = 0; i < words.length; i++) {
            String str = words[i];
            if (map.containsKey(str)) {
                map.get(str).add(i);
            } else {
                List<Integer> indexes = new ArrayList<Integer>();
                indexes.add(i);
                map.put(str, indexes);
            }
        }
    }

    public int shortest(String word1, String word2) {
        List<Integer> list1 = map.get(word1);
        List<Integer> list2 = map.get(word2);
        int min = Integer.MAX_VALUE;
        int i = 0;
        int j = 0;
        while(i < list1.size() && j < list2.size()){
            min = Math.min(min, Math.abs(list1.get(i) - list2.get(j)));
            if(list1.get(i) < list2.get(j)) {
                i++;
            } else {  
                j++;
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
