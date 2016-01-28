[Link](https://leetcode.com/problems/jump-game-ii/)

```java
public class Solution {
    public int jump(int[] nums) {
        if (nums.length == 1) {
            return 0;
        }
        int step = 1;
        int reach = nums[0];
        int index = 1;
        while (reach < nums.length - 1) {
            step++;
            int nextReach = 0;
            while (index <= reach) {
                nextReach = Math.max(nextReach, index + nums[index]);
                index++;
            }
            reach = nextReach;
        }
        return step;
    }
}
```
