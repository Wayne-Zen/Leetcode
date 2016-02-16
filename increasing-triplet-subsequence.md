[Link](https://leetcode.com/problems/increasing-triplet-subsequence/)

```java
public class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums == null) {
            throw new NullPointerException();
        }
        if (nums.length < 3) {
            return false;
        }
        long val1 = nums[0];
        long val2 = Long.MAX_VALUE;
        for (int i = 1; i < nums.length; i++) {
            int val = nums[i];
            if (val <= val1) {
                val1 = val; 
            } else if (val <= val2) {
                val2 = val;
            } else {
                return true;
            }
        }
        return false;
    }
}
```
