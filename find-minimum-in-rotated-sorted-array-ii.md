[Link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)

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
            if (nums[lo] == nums[hi]) {
                lo++;
                continue;
            } else if (nums[lo] < nums[hi]) {
                return nums[lo];
            } 
            if (nums[mid] == nums[lo]) {
                lo++;
                continue;
            }
            if (nums[mid] == nums[hi]) {
                hi--;
                continue;
            }
            if (nums[mid] > nums[lo]) {
                lo = mid;
            } else if (nums[mid] < nums[hi]) {
                hi = mid;
            }
        }
        return Math.min(nums[lo], nums[hi]);
    }
}
```
