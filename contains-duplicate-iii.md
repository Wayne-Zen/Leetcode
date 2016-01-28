[Link](https://leetcode.com/problems/contains-duplicate-iii/)

O(N)

```java
public class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if (k < 1 || t < 0) {
            return false;
        }
        // bucket index -> lastest val
        // 纪录最近的坐标
        // 如果去掉的头元素在window里有相同的值的元素[1, 100, 200, 1, 5]
        // 再slide到取出头元素之前就已经，满足条件返回true了， 所以可以直接remove
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (i > k) {
                map.remove(nums[i - k - 1] / Math.max(1, t));
            }
            int key = nums[i] / Math.max(1, t);
            for (int x : new int[]{key, key - 1, key + 1}) {
                if (map.containsKey(x) && Math.abs(map.get(x) - (long)nums[i]) <= t) {
                    return true;
                }
            }
            map.put(key, nums[i]);
        }
        return false;
    }
}
```

O(NlogK)

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
