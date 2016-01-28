[Link](https://leetcode.com/problems/minimum-size-subarray-sum/)


```java
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int lo = -1; // exclusive
        int hi = -1;
        int sum = 0;
        boolean expand = true;
        int len = Integer.MAX_VALUE;
        while (true) {
            if (expand) {
                hi++;
                if (hi == nums.length) {
                    break;
                }
                sum += nums[hi];
                if (sum >= s) {
                    expand = false;
                    len = Math.min(len, hi - lo);
                } 
            } else {
                lo++;
                sum -= nums[lo];
                if (sum >= s) {
                    len = Math.min(len, hi - lo);
                } else {
                    expand = true;
                }
            }
        }
        if (len == Integer.MAX_VALUE) {
            return 0;
        } else {
            return len;
        }
    }
}
```
