[Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int res = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[res]) {
                nums[res++] = nums[i];
            }
        }
        return res;
    }
}
```
