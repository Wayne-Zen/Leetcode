[Link](https://leetcode.com/problems/contains-duplicate-iii/)

```java
public class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
         if(k < 1 || t < 0)
            return false;
        TreeSet<Integer> set = new TreeSet<Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (i >= k + 1) {
                set.remove(nums[i - k - 1]);
            }
            int n = nums[i];
            if ((set.floor(n) != null && set.floor(n) + t >= n) ||
                    (set.ceiling(n) != null && n + t >= set.ceiling(n))) {
                return true;
            } else {
                set.add(nums[i]);
            }
        }
        return false;
    }
}
```
