[Link](https://leetcode.com/problems/trapping-rain-water/)

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
        int res = 0;
        for (int i = 1; i < height.length; i++) {
            left[i] = Math.max(height[i - 1], left[i - 1]); // 坑： height[i - 1]
            res += Math.max(0, Math.min(right[i], left[i]) - height[i]);
        }

        return res;
    }
}
```
