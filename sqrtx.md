[Link](https://leetcode.com/problems/sqrtx/)

```java
public class Solution {
    public int mySqrt(int x) {
        // find the last number which square of it <= x
        long lo = 0;
        long hi = x;
        while (lo + 1 < hi) {
            long mid = lo + (hi - lo) / 2;
            if (mid * mid == x) {
                return (int)mid;
            } else if (mid * mid < x) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        if (hi * hi <= x) {
            return (int)hi;
        } else {
            return (int)lo;
        }
    }
}
```
