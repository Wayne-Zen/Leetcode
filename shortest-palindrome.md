[Link](https://leetcode.com/problems/shortest-palindrome/)

```java
public class Solution {
    public String shortestPalindrome(String s) {
        StringBuffer rev_s = new StringBuffer(s);
        rev_s = rev_s.reverse();
        StringBuffer l = new StringBuffer();
        l.append(s);
        l.append('#');
        l.append(rev_s);
        int[] p = new int[l.length()];
        for (int i=1; i<l.length(); i++) {
            int j = p[i-1];
            while (j>0 && l.charAt(i) != l.charAt(j)) {
                j = p[j-1];
            }
            p[i] = j + (l.charAt(i)==l.charAt(j) ? 1 : 0);
        }
        StringBuffer res = new StringBuffer();
        res.append(rev_s.substring(0, s.length() - p[p.length-1]));
        res.append(s);
        return res.toString();
    }
}
```
