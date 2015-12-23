[Link](https://leetcode.com/problems/h-index-ii/)

```java
public class Solution {
    public int hIndex(int[] citations) {
        int N = citations.length;
        for (int i = N - 1; i >= 0; i--) {
            if (citations[i] < N - i) {
                return N - i - 1;
            }
        }
        return N;
    }
}
```
