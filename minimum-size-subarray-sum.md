[Link](https://leetcode.com/problems/minimum-size-subarray-sum/)

* 需要纪录是否发现了满足要求的subarray
* expand 和 shrink, 坐标更新与求和的顺序不一样

```java
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int minLen = nums.length;
        int lo = 0;
        int hi = 0;
        int sum = nums[0];
        boolean find = false;
        while (true) {
            if (sum >= s) {
                find = true;
                // try to increase lo
                if (lo < hi) {
                    sum -= nums[lo];
                    minLen = Math.min(minLen, hi - lo + 1);
                    lo++;
                } else {
                    return 1;
                }
            } else { // sum < s
                // try to increase hi
                if (hi + 1 < nums.length) {
                    hi++;
                    sum += nums[hi];
                } else {
                    break;
                }
            }
        }
        if  (find) {
            return minLen;
        } else {
            return 0;
        }
    }
}
```
