[Link](https://leetcode.com/problems/jump-game/)

* greedy

```java
public class Solution {
    public boolean canJump(int[] nums) {
        int cov = 0;
        for (int i = 0; i < nums.length; i++) {
            if (i > cov) {
                return false;
            }
            cov = Math.max(cov, i + nums[i]);
        }
        return true;
    }
}
```
