[Link](https://leetcode.com/problems/find-the-duplicate-number/)

* O(nlogn) 

```java
public class Solution {
    public int findDuplicate(int[] nums) {
        int N = nums.length - 1;
        int lo = 1;
        int hi = N;
        while (lo + 1 < hi) {
            int pivotVal = lo + (hi - lo) / 2;
            int less = less(nums, pivotVal);
            if (less < pivotVal) {
                lo = pivotVal;
            } else if (less >= pivotVal) {
                hi = pivotVal;
            }
        }
        if (less(nums, hi) >= hi) {
            return lo;
        } else {
            return hi;
        }
    }
    private int less(int[] nums, int pivotVal) {
        int less = 0;
        for (int num : nums) {
            if (num < pivotVal) {
                less++;
            } 
        }
        return less;
    }
}
```
