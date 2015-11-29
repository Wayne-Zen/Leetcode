[Link](https://leetcode.com/problems/h-index/)

```java
public class Solution {
    public int hIndex(int[] citations) {
        Integer[] cite = new Integer[citations.length];
        for (int i = 0; i < cite.length; i++) {
            cite[i] = citations[i];
        }
        Arrays.sort(cite, Collections.reverseOrder());
        for (int i = 0; i < cite.length; i++) {
            if (i >= cite[i]) {
                return i;
            }
        }
        return cite.length;
    }
}
```
