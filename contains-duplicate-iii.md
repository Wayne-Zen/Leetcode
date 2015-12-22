[Link](https://leetcode.com/problems/contains-duplicate-iii/)

```java
public class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        TreeSet<Integer> set = new TreeSet<Integer>();
        for(int i = 0; i < nums.length; i++){
            int val = nums[i];
            //  least element in this set greater than or equal to the given element
            if(set.ceiling(val) != null && set.ceiling(val) <= val + t) return true;
            // greatest element in this set less than or equal to the given element
            if(set.floor(val) != null && set.floor(val) >= val - t) return true;
            set.add(val);
            if (set.size() > k) {
                set.remove(nums[i - k]);
            }
        }
        return false;
    }
}
```
