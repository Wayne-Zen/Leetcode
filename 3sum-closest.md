[Link](https://leetcode.com/problems/3sum-closest/)

```java
public class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int res = 0;
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < nums.length; i++) {
            int head = i + 1;
            int tail = nums.length - 1;
            while (head < tail) {
                int sum = nums[i] + nums[head] + nums[tail];
                int diff = target - sum;
                if (Math.abs(diff) < min) {
                    min = Math.abs(diff);
                    res = sum;
                }
                
                if (diff < 0) {
                    tail--;
                } else if (diff > 0) {
                    head++;
                } else {
                    return target;
                }
            }
        }
        return res;
    }
}
```
