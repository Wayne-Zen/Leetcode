[Link](https://leetcode.com/problems/valid-palindrome/)

```java
public class Solution {
    public boolean isPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }
        s = s.toLowerCase();
        int lo = 0;
        int hi = s.length() - 1;
        while (lo < hi) {
            char c1 = s.charAt(lo);
            char c2 = s.charAt(hi);
            if (!Character.isLetterOrDigit(c1)) {
                lo++;
                continue;
            }
            if (!Character.isLetterOrDigit(c2)) {
                hi--;
                continue;
            }
            if (c1 != c2) {
                return false;
            } else {
                lo++;
                hi--;
            }
        }
        return true;
    }
}
```
