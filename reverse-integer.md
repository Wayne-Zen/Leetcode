[Link](https://leetcode.com/problems/reverse-integer/)

```java
public class Solution {
    public int reverse(int x) {
        long res = 0;
        int sign = x < 0 ? -1 : 1;
        long xl = Math.abs((long)x);
        while (xl > 0) {
            res = res * 10 + (xl % 10);
            xl /= 10;
        }
        res = sign * res;
        if (res > Integer.MAX_VALUE || res < Integer.MIN_VALUE) {
            return 0;
        } else {
            return (int)res;
        }
    }
}
```
