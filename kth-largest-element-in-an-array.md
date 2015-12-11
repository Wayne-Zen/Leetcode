[Link](https://leetcode.com/problems/kth-largest-element-in-an-array/)

```java
public class Solution {
    public int findKthLargest(int[] nums, int k) {
        int lo = 0; 
        int hi = nums.length - 1;
        while (true) {
            int index = partition(nums, lo, hi);
            if (index == k - 1) {
                return nums[index];
            } else if (index > k - 1) {
                hi = index - 1;
            } else {
                lo = index + 1;
            }
        }
    }
    private int partition(int[] nums, int lo, int hi) {
        int val = nums[hi];
        for (int i = lo; i < hi; i++) {
            if (nums[i] > val) {
                swap(nums, lo, i);
                lo++;
            }
        }
        swap(nums, lo, hi);
        return lo;
    }
    private void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp;
    }
}
```
