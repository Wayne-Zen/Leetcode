[Link](https://leetcode.com/problems/search-for-a-range/)

<img src="img/Photos/search-for-a-range.png" width="400">

```java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] res = new int[2];
        // first nums[i] == target
        int lo = 0;
        int hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] < target) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        if (nums[lo] == target) {
            res[0] = lo;
        } else if (nums[hi] == target) {
            res[0] = hi;
        } else {
            return new int[]{-1, -1};
        }
        // last nums[i] == target
        lo = 0;
        hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] <= target) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        if (nums[hi] == target) {
            res[1] = hi;
        } else if (nums[lo] == target) {
            res[1] = lo;
        } else {
            return new int[]{-1, -1};
        }
        
        return res;
    }
}
```
