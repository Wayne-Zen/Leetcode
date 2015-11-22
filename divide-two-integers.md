[Link](https://leetcode.com/problems/divide-two-integers/)

```java
public class Solution {
    public int divide(int dividend, int divisor) {
        if (dividend == Integer.MIN_VALUE && divisor == -1) {
            return Integer.MAX_VALUE;
        }
        long dv = Math.abs((long)dividend);
        long ds = Math.abs((long)divisor);
        long remain = dv;
        long res = 0;
        while (remain >= ds) {
            int sh = -1;
            long v = remain;
            while (v >= ds) {
                v >>= 1;
                sh++;
            }
            remain -= ds << sh;
            res += 1 << sh;
        }
        
        if ((divisor > 0) != (dividend > 0)) {
            res = -res;
        }
        return (int)res;
    }
}
```
