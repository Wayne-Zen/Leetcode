[Link](https://leetcode.com/problems/maximum-product-of-word-lengths/)

```java
public class Solution {
    public int maxProduct(String[] words) {
        // O(n^2)
        int N = words.length;
        int[] vals = new int[N];
        for (int i = 0; i < N; i++) {
            for (char c : words[i].toCharArray()) {
                vals[i] |= 1 << (c - 'a');
            }
        }
        int max = 0;
        for (int i = 0; i < N; i++) {
            for (int j = i + 1; j < N; j++) {
                if ((vals[i] & vals[j]) == 0) {
                    max = Math.max(max, words[i].length() * words[j].length());
                }
            }
        }
        return max;
    }
}
```
