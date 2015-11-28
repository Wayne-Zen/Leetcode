[Link](https://leetcode.com/problems/house-robber-ii/)

```java
public class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        if (nums.length == 1) {
            return nums[0];
        }
        if (nums.length == 2) {
            return Math.max(nums[0], nums[1]);
        }
        return Math.max(myRob(nums, 0, nums.length - 2),
                        myRob(nums, 1, nums.length - 1));
    }
    
    public int myRob(int[] nums, int start, int end) {
        int[] dp = new int[end - start + 2];
        dp[0] = 0;
        dp[1] = nums[start];
        for (int i = 2; i < dp.length; i++) {
            dp[i] = Math.max(nums[start + i - 1] + dp[i - 2], dp[i - 1]);
        }
        return dp[dp.length - 1];
    }
}
```
