[Link](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

```java
public class Solution {
    public boolean search(int[] nums, int target) {
        int lo = 0; 
        int hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[mid] > nums[lo]) {
                if (nums[lo] <= target && target < nums[mid]) {
                    hi = mid;
                } else {
                    lo = mid;
                }
            } else if (nums[mid] < nums[hi]) {
                if (nums[mid] < target && target <= nums[hi]) {
                    lo = mid;
                } else {
                    hi = mid;
                }
                
            } else if (nums[mid] == nums[lo]) {
                lo++;
            } else if (nums[mid] == nums[hi]) {
                hi--;
            }
        }
        if (nums[hi] == target) {
            return true;
        }
        if (nums[lo] == target) {
            return true;
        }
        return false;
    }
}
```
