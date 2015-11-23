[Link](https://leetcode.com/problems/search-insert-position/)


```java
public class Solution {
    public int searchInsert(int[] nums, int target) {
        //first elememt nums[i] >= target
        int lo = 0; 
        int hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] >= target) {
                hi = mid;
            } else {
                lo = mid;
            }
        }
        if (nums[lo] >= target) {
            return lo;
        } 
        if (nums[hi] >= target){
            return hi;
        }
        return nums.length;
    }
}
```
