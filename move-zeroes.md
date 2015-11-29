[Link](https://leetcode.com/problems/move-zeroes/)

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        int lo = 0;
        int hi = nums.length - 1;
        for (int i = 0; i <= hi; i++) {
            if (nums[i] != 0) {
                swap(nums, i, lo);
                lo++;
            }
        }
    }
    private void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp;
    }
}
```
