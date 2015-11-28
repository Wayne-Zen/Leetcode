[Link](https://leetcode.com/problems/excel-sheet-column-number/)

```java
public class Solution {
    public int titleToNumber(String s) {
        int res = 0;
        int base = 1;
        for (int i = s.length() - 1; i >= 0; i--) {
            char c = s.charAt(i);
            res += (c - 'A' + 1) * base;
            base *= 26;
        }
        return res;
    }
}
```
