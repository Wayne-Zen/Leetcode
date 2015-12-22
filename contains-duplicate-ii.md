[Link](https://leetcode.com/problems/contains-duplicate-ii/)

```java
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        // val -> index
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            int val = nums[i];
            if (map.containsKey(val) && (i - map.get(val)) <= k) {
                return true;
            }
            map.put(val, i);
        }
        return false;
    }
}
```

```java
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Set<Integer> set = new HashSet<Integer>();
        for(int i = 0; i < nums.length; i++){
            int val = nums[i];
            if(set.contains(val)) {
                return true;
            }
            set.add(val);
            if (set.size() > k) {
                set.remove(nums[i - k]);
            }
        }
        return false;
    }
}
```
