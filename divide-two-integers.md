[Link](https://leetcode.com/problems/divide-two-integers/)

```java
public class Solution {
    public int divide(int dividend, int divisor) {
        if (dividend == 0) return 0;
        if (divisor == 0) throw new IllegalArgumentException();
        
        long dd = Math.abs((long)dividend);
        long ds = Math.abs((long)divisor);
        long res = 0;
        while (dd >= ds) {
            long mul = 1;
            long dsSave = ds;
            while (dd >= ds) {
                ds <<= 1;
                mul <<= 1;
            }
            res += mul >> 1;
            dd -= ds >> 1;
            ds = dsSave;
        }
        if ((dividend > 0) != (divisor > 0)) {
            res = -res;
        } 
        if (res > Integer.MAX_VALUE) {
            return Integer.MAX_VALUE;
        } else if (res < Integer.MIN_VALUE) {
            return Integer.MIN_VALUE;
        } else {
            return (int)res;
        }
    }
}
```
