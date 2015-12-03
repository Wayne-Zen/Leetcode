[Link](https://leetcode.com/problems/3sum-smaller/)

```java
public class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        int res = 0;
        if (nums == null || nums.length == 0) {
            return res;
        }
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            int lo = i + 1;
            int hi = nums.length - 1;
            while (lo < hi) {
                if (nums[i] + nums[lo] + nums[hi] < target) {
                    res += hi - lo; // 坑
                    lo++;
                } else {
                    hi--;
                }
            }
        }
        return res;
    }
}
```
