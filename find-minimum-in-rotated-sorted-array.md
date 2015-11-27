[Link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

```java
public class Solution {
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int lo = 0;
        int hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[lo] < nums[hi]) {
                hi = mid;
            } else {
                if (nums[lo] < nums[mid]) {
                    lo = mid;
                } else if (nums[mid] < nums[hi]) {
                    hi = mid;
                }
            }
        }
        return Math.min(nums[lo], nums[hi]);
    }
}
```
