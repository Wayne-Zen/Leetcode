[Link](https://leetcode.com/problems/shortest-word-distance/)

```java
public class Solution {
    public int shortestDistance(String[] words, String word1, String word2) {
        int i1 = -1;
        int i2 = -1;
        int min = words.length + 1;
        for (int i = 0; i < words.length; i++) {
            if (words[i].equals(word1)) {
                i1 = i;
                if (i2 != -1) {
                    min = Math.min(min, i1 - i2);
                }
            }
            if (words[i].equals(word2)) {
                i2 = i;
                if (i1 != -1) {
                    min = Math.min(min, i2 - i1);
                }
            }
        }
        return min;
    }
}
```
