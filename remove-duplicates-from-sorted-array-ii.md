[Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null) {
            return 0;
        }
        if (nums.length <= 2) {
            return nums.length;
        }
        int cnt = 1;
        int loc = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) {
                if (cnt == 1) {
                    nums[loc] = nums[i];
                    loc++;
                    cnt++;
                }
            } else {
                cnt = 1;
                nums[loc] = nums[i];
                loc++;
            }
        }
        return loc;
    }
}
```
