[Link](https://leetcode.com/problems/first-bad-version/)

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int lo = 1;
        int hi = n;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            boolean res = isBadVersion(mid);
            if (res) {
                hi = mid;
            } else {
                lo = mid;
            }
        }
        if (isBadVersion(lo)) {
            return lo;
        } else {
            return hi;
        }
    }
}
```
