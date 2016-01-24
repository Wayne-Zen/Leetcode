[Link](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/)

```java
public class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        //rs_hi - rs_lo = subarray sum = k
        int[] rs = new int[nums.length + 1];
        // val -> index;
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(0, 0);
        for (int i = 1; i < rs.length; i++) {
            rs[i] = rs[i - 1] + nums[i - 1];
            if (!map.containsKey(rs[i])) {
                map.put(rs[i], i);
            }
        }
        int max = 0;
        for (int i = 1; i < rs.length; i++) {
            int target = rs[i] - k;
            if (map.containsKey(target)) {
                max = Math.max(max, i - map.get(target));
            }
        }
        return max;
    }
}
```
