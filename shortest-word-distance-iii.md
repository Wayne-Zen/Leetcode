[Link](https://leetcode.com/problems/shortest-word-distance-iii/)

```java
public class Solution {
    public int shortestWordDistance(String[] words, String word1, String word2) {
        int index1 = -1;
        int index2 = -1;
        int min = words.length;
        
        if (word1.equals(word2)) {
            for (int i = 0; i < words.length; i++) {
                if (word1.equals(words[i])) {
                    if (index1 == -1) {
                        index1 = i;
                    } else {
                        int len = i - index1;
                        min = Math.min(min, len);
                        index1 = i;
                    }
                }
            }
        } else {
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
        }
        
        
        return min;
    }
}
```
