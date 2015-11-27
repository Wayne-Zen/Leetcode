[Link](https://leetcode.com/problems/maximum-gap/)

```java
public class Solution {
    public int maximumGap(int[] nums) {
        if (nums == null || nums.length < 2) {
            return 0;
        }
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            min = Math.min(min, nums[i]);
            max = Math.max(max, nums[i]);
        }
        
        int width = (max - min) / nums.length + 1; // KEY
        int[][] buckets = new int[(max - min) / width + 1][2];
        for (int[] pair : buckets) {
            pair[0] = -1;
            pair[1] = -1;
        }
        for (int x : nums) {
            int i = (x - min) / width;
            if (buckets[i][0] == -1) {
                buckets[i][0] = x;
                buckets[i][1] = x;
            } else {
                buckets[i][0] = Math.min(buckets[i][0], x);
                buckets[i][1] = Math.max(buckets[i][1], x);
            }
        }
        int maxGap = -1;
        int last = 0;
        for (int i = 0; i < buckets.length; i++) {
            if (buckets[i][0] != -1) {
                if (maxGap == -1) {
                    last = buckets[i][1];
                    maxGap = 0;
                } else {
                    maxGap = Math.max(maxGap, buckets[i][0] - last);
                    last = buckets[i][1];
                }
            }
        }
        return maxGap;
    }
}
```
