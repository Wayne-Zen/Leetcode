[Link](https://leetcode.com/problems/longest-palindromic-substring/)

```java
public class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }
        int[] t = new int[2 * s.length() + 1];
        for (int i = 0; i < s.length(); i++) {
            t[2 * i] = Integer.MAX_VALUE;
            t[2 * i + 1] = s.charAt(i);
        }
        t[2 * s.length()] = Integer.MAX_VALUE;
        int[] p = new int[t.length];
        for (int i = 0; i < t.length; i++) {
            while (i + p[i] + 1 < t.length 
                    && i - p[i] - 1 >= 0 
                    && t[i + p[i] + 1] == t[i - p[i] - 1]) {
                p[i]++;
            }
        }
        int center = 0;
        int width = 0;
        for (int i = 0; i < p.length; i++) {
            if (p[i] > width) {
                width = p[i];
                center = i;
            }
        }
        return s.substring((center - width) / 2, (center + width) / 2);
    }
}
```


```java
public class Solution {
    // Manacher
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }
        int[] t = new int[2 * s.length() + 1];
        for (int i = 0; i < s.length(); i++) {
            t[2 * i] = Integer.MAX_VALUE;
            t[2 * i + 1] = s.charAt(i);
        }
        t[2 * s.length()] = Integer.MAX_VALUE;
        
        int[] p = new int[t.length];
        int center = 0;
        int right = 0;
        for (int i = 0; i < t.length; i++) {
            if (right > i) {
                int mirror = 2*center - i;
                p[i] = Math.min(right - i, p[mirror]);
            }
            
            // attempt to expand palindrome centered at i
            while (i + p[i] + 1 < t.length 
                    && i - p[i] - 1 >= 0 
                    && t[i + p[i] + 1] == t[i - p[i] - 1]) {
                p[i]++;
            }
                
            // if palindrome centered at i expands past right,
            // adjust center based on expanded palindrome.
            if (i + p[i] > right) {
                center = i;
                right = i + p[i];
            }
        }
        
        int width = 0;
        for (int i = 0; i < p.length; i++) {
            if (p[i] > width) {
                width = p[i];
                center = i;
            }
        }

        return s.substring((center - width) / 2, (center + width) / 2);
    }
}
```
