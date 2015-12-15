[Link](https://leetcode.com/problems/implement-strstr/)

```java
public class Solution {
    public int strStr(String haystack, String needle) {
        if (haystack == null || needle == null) {
            return -1;
        }
        int n = haystack.length();
        int m = needle.length();
        for (int i = 0; i < n - m + 1; i++) {
            int j = 0;
            for (; j < m; j++) {
                if (haystack.charAt(i + j) != needle.charAt(j)) {
                    break;
                }
            }
            if (j == m) {
                return i;
            }
        }
        return -1;
    }
}
```

```java
class Solution {
    /**
     * Returns a index to the first occurrence of target in source,
     * or -1  if target is not part of source.
     * @param source string to be scanned.
     * @param target string containing the sequence of characters to match.
     */
    public int strStr(String source, String target) {
        if (source == null || target == null) {
            return -1;
        }
        if (target.length() == 0) {
            return 0;
        }
        int[] next = getPattern(target);
        int j = 0;
        for (int i = 0; i < source.length(); i++) {
            while (j != 0 && source.charAt(i) != target.charAt(j)) {
                j = next[j - 1]; // key point
            }
            if (source.charAt(i) == target.charAt(j)) {
                j++;
                if (j == target.length()) {
                    return i - target.length() + 1;
                }
            }
        }
        return -1;
    }
    
    private int[] getPattern(String target) {
        int[] res = new int[target.length()];
        res[0] = 0;
        int j = 0;
        for (int i = 1; i < target.length(); i++) {
            while (j != 0 && target.charAt(j) != target.charAt(i)) {
                j = res[j - 1];
            }
            if (target.charAt(i) == target.charAt(j)) {
                j++;
                res[i] = j;
            } 
        }
        return res;
    }
}
```
