[Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int res = 1;
        int cnt = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[res - 1]) {
                nums[res++] = nums[i];
                cnt = 1;
            } else if (cnt == 1) {
                nums[res++] = nums[i];
                cnt++;
            }
        }
        return res;
    }
}
```
