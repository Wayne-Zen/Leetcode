[Link](https://leetcode.com/problems/patching-array/)

```java
public class Solution {
    public int minPatches(int[] nums, int n) {
        long miss = 1;
        int cnt = 0, index = 0;
        while (miss <= n) {
            if (index < nums.length && nums[index] <= miss) {
                miss += nums[index++];
            } else {
                miss <<= 1;
                cnt++;
            }
        }
        return cnt;
    }
}
```
