[Link](https://leetcode.com/problems/jump-game-ii/)

```java
public class Solution {
    public int jump(int[] nums) {
        int step = 0;
        int lastCov = 0; // last coverage
        int curCov = 0;  // current coverage
        for (int i = 0; i < nums.length; ++i) {
            if (i > lastCov) {
                lastCov = curCov;
                ++step;
            }
            curCov = Math.max(curCov, i + nums[i]);
        }

        return step;
    }
}
```
