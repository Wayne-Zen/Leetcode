[Link](https://leetcode.com/problems/h-index-ii/)

```java
public class Solution {
    public int hIndex(int[] citations) {
        if (citations == null || citations.length == 0) {
            return 0;
        }
        int lo = 0;
        int hi = citations.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            int paperNum = citations.length - mid;
            int citationNum = citations[mid];
            if (paperNum > citationNum) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        return Math.max(Math.min(citations.length - hi, citations[hi]),
                        Math.min(citations.length - lo, citations[lo]));
    }
}
```
