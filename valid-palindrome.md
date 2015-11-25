[Link](https://leetcode.com/problems/valid-palindrome/)

```java
public class Solution {
    public boolean isPalindrome(String s) {
        s = s.toUpperCase();
        int lo = 0;
        int hi = s.length() - 1;
        while (lo <= hi) {
            if (!Character.isDigit(s.charAt(lo)) && !Character.isLetter(s.charAt(lo))) {
                lo++;
                continue;
            }
            if (!Character.isDigit(s.charAt(hi)) && !Character.isLetter(s.charAt(hi))) {
                hi--;
                continue;
            }
            if (s.charAt(lo) != s.charAt(hi)) {
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
