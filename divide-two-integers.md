[Link](https://leetcode.com/problems/divide-two-integers/)

```java
public class Solution {
    public int divide(int dividend, int divisor) {
        if (dividend == Integer.MIN_VALUE && divisor == -1) {
            return Integer.MAX_VALUE;
        }
        long dv = Math.abs((long)dividend);
        long ds = Math.abs((long)divisor);
        long res = 0;
        while (dv >= ds) {
            int shift = -1;
            while (dv >= (ds << (shift + 1))) {
                shift++;
            }
            dv -= ds << shift;
            res += 1 << shift;
        }
        if ((dividend > 0) != (divisor > 0)) {
            res = -res;
        }
        return (int)res;
    }
}
```
