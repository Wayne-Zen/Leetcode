[Link](https://leetcode.com/problems/summary-ranges/)

```java
public class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> res = new ArrayList<String>();
        if (nums == null || nums.length == 0) {
            return res;
        }
        int lo = 0;
        for (int i = 1; i < nums.length; i++) {
            if (i - lo == nums[i] - nums[lo]) {
                continue;
            } else {
                if (nums[i - 1] == nums[lo]) {
                    res.add(nums[lo] + "");
                } else {
                    res.add(nums[lo] + "->" + nums[i - 1]);
                }
                lo = i;
            }
        }
        if (lo == nums.length - 1) {
            res.add(nums[lo] + "");
        } else {
            res.add(nums[lo] + "->" + nums[nums.length - 1]);
        }
        return res;
    }
}
```
