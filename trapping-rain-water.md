[Link](https://leetcode.com/problems/trapping-rain-water/)

* A[left] = max{A[j], j<i}, A[right] = max{A[j], j>i}
* Hmin = min(A[left], A[right])
* S[i] = Math.max(0, Hmin - A[i])

```java
public class Solution {
    public int trap(int[] height) {
        if (height == null || height.length == 0) {
            return 0;
        }
        
        int[] right = new int[height.length];
        right[right.length - 1] = 0;
        for (int i = height.length - 2; i >= 0; i--) {
            right[i] = Math.max(height[i + 1], right[i + 1]); // 坑： height[i + 1]
        }
        
        int[] left = new int[height.length];
        left[0] = 0;
        for (int i = 1; i < height.length; i++) {
            left[i] = Math.max(height[i - 1], left[i - 1]); // 坑： height[i - 1]
        }
        
        int res = 0;
        for (int i = 0; i < height.length; i++) {
            int h = Math.min(right[i], left[i]);
            res += Math.max(0, h - height[i]);
        }
        return res;
    }
}
```
