[Link](https://leetcode.com/problems/shortest-word-distance/)

```java
public class Solution {
    public int shortestDistance(String[] words, String word1, String word2) {
        int index1 = -1;
        int index2 = -1;
        int min = words.length;
        for (int i = 0; i < words.length; i++) {
            if (word1.equals(words[i])) {
                index1 = i;
                if (index2 != -1) {
                    int len = index1 - index2;
                    min = Math.min(min, len);
                }
            }
            if (word2.equals(words[i])) {
                index2 = i;
                if (index1 != -1) {
                    int len = index2 - index1;
                    min = Math.min(min, len);
                }
            }
        }
        return min;
    }
}
```
