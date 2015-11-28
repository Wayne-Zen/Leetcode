[Link](https://leetcode.com/problems/summary-ranges/)

```java
public class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> res = new ArrayList<String>();
        int N = nums.length;
        int start = 0;
        while (start < N) {
            int len = 1;
            while (start + len < N && nums[start] + len == nums[start + len]) {
                len++;
            }
            if (len == 1) {
                res.add(String.valueOf(nums[start]));
            } else {
                res.add(nums[start] + "->" + nums[start + len - 1]);
            }
            start += len;
        }
        return res;
    }
}
```
