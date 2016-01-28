[Link](https://leetcode.com/problems/contains-duplicate-ii/)

```java
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        // val -> index
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            int val = nums[i];
            if (!map.containsKey(val)) {
                map.put(val, i);
            } else {
                if (Math.abs(i - map.get(val)) <= k) {
                    return true;
                } else {
                    map.put(val, i);
                }
            }
        }
        return false;
    }
}
```
