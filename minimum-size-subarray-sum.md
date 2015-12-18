[Link](https://leetcode.com/problems/minimum-size-subarray-sum/)

* 需要纪录是否发现了满足要求的subarray
* expand 和 shrink, 坐标更新与求和的顺序不一样

```java
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if (nums == null || nums.length == 0 || s <= 0) {
            return 0;
        }
        int len = nums.length + 1;
        int lo = -1; // exclusive
        int hi = -1;
        int sum = 0;
        while (true) {
            if (sum < s) {
                hi++;
                if (hi == nums.length) {
                    break;
                }
                sum += nums[hi];
            } else {
                lo++;
                sum -= nums[lo];
            }
            if (sum >= s) {
                len = Math.min(len, hi - lo);
                if (len == 1) {
                    return 1;
                }
            }
        }
        if (len == nums.length + 1) {
            return 0;
        }
        return len;
    }
}
```
