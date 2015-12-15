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
    public int strStr(String haystack, String needle){
        if (haystack == null || needle == null)
            return -1;
        //generate next array, need O(n) time
        int i = -1, j = 0, m = haystack.length(), n = needle.length();
        int[] next = new int[n];
        if (next.length > 0) 
            next[0] = -1;
        while (j < n - 1) {
            if (i == -1 || needle.charAt(i) == needle.charAt(j))
                next[++j] = ++i;
            else 
                i = next[i];
        }
        //check through the haystack using next, need O(m) time
        i = 0; j = 0;
        while (i < m && j < n) {
            if (j == -1 || haystack.charAt(i) == needle.charAt(j)) {
                i++;
                j++;
            }
            else 
                j = next[j];
        }
        if (j == n)
            return i - j;
        return -1;
    }
}
```
