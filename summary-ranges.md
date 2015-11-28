[Link](https://leetcode.com/problems/summary-ranges/)

```java
public class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> res = new ArrayList<String>();
        if (nums == null || nums.length == 0) {
            return res;
        }
        if (nums.length == 1) {
            res.add(nums[0] + "");
            return res;
        } // [1]
        int start = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > nums[i - 1] + 1 ) { // overflow
                // close
                if (nums[i - 1] == start) {
                    res.add(String.valueOf(start));
                    start = nums[i];
                } else {
                    res.add(start + "->" + nums[i - 1]);
                    start = nums[i];
                }
            }
            if (i == nums.length - 1) {
                if (nums[i] > nums[i - 1] + 1) {
                    res.add(String.valueOf(nums[i]));
                } else {
                    res.add(start + "->" + nums[i]);
                }
            }
        }
        return res;
    }
}
```
