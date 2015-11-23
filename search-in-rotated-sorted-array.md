[Link](https://leetcode.com/problems/search-in-rotated-sorted-array/)

* 注意target等于nums[hi] nums[lo]

```java
public class Solution {
    public int search(int[] nums, int target) {
        int lo = 0;
        int hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[mid] > nums[lo]) {
                if (nums[lo] <= target && target < nums[mid]) {
                    hi = mid;
                } else {
                    lo = mid;
                }
            } else { // nums[mid] < nums[hi]
                if (nums[mid] < target && target <= nums[hi]) {
                    lo = mid;
                } else {
                    hi = mid;
                }
            }
        }
        if (nums[hi] == target) {
            return hi;
        }
        if (nums[lo] == target) {
            return lo;
        }
        return -1;
    }
}
```
