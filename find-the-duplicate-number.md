[Link](https://leetcode.com/problems/find-the-duplicate-number/)

```java
public class Solution {
    public int findDuplicate(int[] nums) {
        Arrays.sort(nums);
        int N = nums.length;
        int lo = 0;
        int hi = N - 1;
        while (lo + 1 < hi) {
            int pivotIndex = lo + (hi - lo) / 2;
            int pivotVal = nums[pivotIndex];
            //System.out.println(pivotVal);
            int[] cnt = count(nums, pivotVal);
            if (cnt[0] <= pivotVal - 1 && cnt[1] >= N - pivotVal) {
                lo = pivotIndex;
            } else if (cnt[0] >= pivotVal && cnt[1] <= N - pivotVal - 1) {
                hi = pivotIndex;
            } else {
                return pivotVal;
            }
        }
        int[] cnt = count(nums, nums[lo]);
        if (cnt[0] == lo - 1 && cnt[1] == N - lo) {
            return nums[hi];
        } else {
            return nums[lo];
        }
    }
    private int[] count(int[] nums, int pivotVal) {
        int less = 0;
        int greater = 0;
        for (int num : nums) {
            if (num < pivotVal) {
                less++;
            } 
            if (num > pivotVal) {
                greater++;
            }
        }
        return new int[]{less, greater};
    }
}
```
