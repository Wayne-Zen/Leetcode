[Link](https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/)

```java
public class Solution {
    public int minArea(char[][] image, int x, int y) {
        if (image == null || image.length == 0 || image[0].length == 0) {
            return 0;
        }
        int m = image.length;
        int n = image[0].length;
        int lo = 0;
        int hi = 0;
        int hFirst = 0;
        int hLast = 0;
        int vFirst = 0;
        int vLast = 0;
        
        // hFirst
        lo = 0;
        hi = y;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (checkOneVirtical(image, mid)) {
                hi = mid;
            } else {
                lo = mid;
            }
        }
        hFirst = checkOneVirtical(image, lo) ? lo : hi;
        
        // hLast
        lo = y;
        hi = n - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (checkOneVirtical(image, mid)) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        hLast = checkOneVirtical(image, hi) ? hi : lo;
        
        //vFirst
        lo = 0;
        hi = x;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (checkOneHorizon(image, mid)) {
                hi = mid;
            } else {
                lo = mid;
            }
        }
        vFirst = checkOneHorizon(image, lo) ? lo : hi;
        
        //vLast
        lo = x;
        hi = m - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (checkOneHorizon(image, mid)) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        vLast = checkOneHorizon(image, hi) ? hi : lo;
        
        return (hLast + 1 - hFirst) * (vLast + 1 - vFirst);
    }
    
    private boolean checkOneVirtical(char[][] image, int c) {
        for (int i = 0; i < image.length; i++) {
            if (image[i][c] == '1') {
                return true;
            }
        }
        return false;
    }
    private boolean checkOneHorizon(char[][] image, int r) {
        for (int i = 0; i < image[0].length; i++) {
            if (image[r][i] == '1') {
                return true;
            }
        }
        return false;
    }
}
```
