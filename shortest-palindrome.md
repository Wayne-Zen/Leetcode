[Link](https://leetcode.com/problems/shortest-palindrome/)

```java
public class Solution {
    public String shortestPalindrome(String s) {
        int n = s.length();
        int[] v = new int[2 * n + 1];
        int pos = 0;
        for (int i = 0; i < n; i++) {
            v[pos++] = s.charAt(i);
        }
        v[pos++] = Integer.MAX_VALUE;
        for (int i = n - 1; i >= 0; i--) {
            v[pos++] = s.charAt(i);
        }
        int j = 0;
        int[] p = new int[v.length];
        for (int i = 1; i < v.length; i++) {
            while (j != 0 && v[j] != v[i]) {
                j = p[j - 1];
            }
            if (v[j] == v[i]) {
                j++;
                p[i] = j;
            }
        }
        StringBuilder sb = new StringBuilder();
        for (int i = n + 1; i < n + 1 + n - p[p.length - 1]; i++) {
            sb.append((char)v[i]);
        }
        sb.append(s);
        return sb.toString();
    }
}
```
