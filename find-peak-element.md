[Link](https://leetcode.com/problems/find-peak-element/)

```java
public class Solution {
    public int findPeakElement(int[] nums) {
        int lo = 0;
        int hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] > nums[mid - 1] && nums[mid] > nums[mid + 1]) {
                return mid;
            } else if (nums[mid] < nums[mid + 1]) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        if (nums[hi] > nums[lo]) {
            return hi;
        } else {
            return lo;
        }
    }
}
```
