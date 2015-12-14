[Link](https://leetcode.com/problems/reverse-bits/)

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int lo = 0;
        int hi= 31;
        while (lo < hi) {
            n = swap(n, lo, hi);
            lo++;
            hi--;
        }
        return n;
    }
    private int swap(int n, int lo, int hi) {
        int a = (n >> lo) & 1;
        int b = (n >> hi) & 1;
        if (a != b) {
            return n ^ (1 << lo | 1 << hi);
        } else {
            return n;
        }
    }
}
```
