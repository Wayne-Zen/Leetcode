[Link](https://leetcode.com/problems/rotate-array/)

```java
public class Solution {
    public void rotate(int[] nums, int k) {
        if (nums == null 
                || nums.length == 0
                || nums.length == 1
                || k == 0) {
            return;
        }
        k = k % nums.length;
        reverse(nums, 0, nums.length - k - 1);
        reverse(nums, nums.length - k, nums.length - 1);
        reverse(nums, 0, nums.length - 1);
    }
    
    private void reverse(int[] nums, int lo, int hi) {
        while (lo < hi) {
            int temp = nums[lo];
            nums[lo] = nums[hi];
            nums[hi] = temp;
            lo++;
            hi--;
        }
    }
}
```
