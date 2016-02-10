[Link](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/)

```java
public class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int[] sums = new int[nums.length + 1];
        // sum -> index
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(0, 0);
        int max = 0;
        for (int i = 1; i < sums.length; i++) {
            sums[i] = nums[i - 1] + sums[i - 1];
            // sums[i] - target = k
            int target = sums[i] - k;
            if (map.containsKey(target)) {
                max = Math.max(max, i - map.get(target));
            }
            if (!map.containsKey(sums[i])) {
                map.put(sums[i], i);
            }
        }
        return max;
    }
}
```
