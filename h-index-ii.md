[Link](https://leetcode.com/problems/h-index-ii/)

```java
public class Solution {
    public int hIndex(int[] citations) {
        int N = citations.length;
        if (N == 0) {
            return 0;
        }
        int lo = 0;
        int hi = N - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (N - mid <= citations[mid]) {
                hi = mid;
            } else {
                lo = mid;
            }
        }
        if (N - lo <= citations[lo]) {
            return N - lo;
        } else if (N - hi <= citations[hi]) {
            return N - hi;
        }
        return 0;
    }
}
```

```java
public class Solution {
    public int hIndex(int[] citations) {
        int N = citations.length;
        for (int i = N - 1; i >= 0; i--) {
            if (citations[i] < N - i) {
                return N - i - 1;
            }
        }
        return N;
    }
}
```
