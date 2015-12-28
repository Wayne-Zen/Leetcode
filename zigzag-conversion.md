[Link](https://leetcode.com/problems/zigzag-conversion/)

```java
public class Solution {
    public String convert(String s, int numRows) {
        if (numRows == 1) {
            return s;
        }
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < numRows; i++) {
            int size = 2 * numRows - 2;
            for (int j = i; j < s.length(); j+=size) {
                if (i == 0 || i == numRows - 1) {
                    sb.append(s.charAt(j));
                } else {
                    int loc1 = j;
                    int loc2 = j + size - 2 * i;
                    sb.append(s.charAt(loc1));
                    if (loc2 < s.length()) {
                        sb.append(s.charAt(loc2));
                    }
                }
            }
        }
        return sb.toString();
    }
}
```
