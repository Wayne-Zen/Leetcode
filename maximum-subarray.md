[Link](https://leetcode.com/problems/maximum-subarray/)


```java
public class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int maxSum = nums[0];
        int curSum = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (curSum <= 0) {
                curSum = 0;
            }
            curSum = curSum + nums[i];
            if (curSum > maxSum) {
                maxSum = curSum;
            }
        }
        return maxSum;
    }
}
```
