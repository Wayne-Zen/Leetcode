[Link](https://leetcode.com/problems/maximum-gap/)

```java
public class Solution {
    public int maximumGap(int[] nums) {
        if (nums == null || nums.length < 2) {
            return 0;
        }
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            min = Math.min(min, nums[i]);
            max = Math.max(max, nums[i]);
        }
        int width = Math.max(1, (max - min) / (nums.length - 1)); 
        ArrayList<ArrayList<Integer>> buckets = new ArrayList<ArrayList<Integer>>();
        for (int i = 0; i < (max - min) / width + 1; i++) {
            buckets.add(new ArrayList<Integer>());
        }
        for (int x : nums) {
            int index = (x - min) / width;
            buckets.get(index).add(x);
        }
        int gap = 0;
        ArrayList<Integer> last = new ArrayList<Integer>();
        for (int i = 0; i < (max - min) / width + 1; i++) {
            ArrayList<Integer> now = buckets.get(i);
            if (now.size() != 0) {
                if (last.size() != 0) {
                    gap = Math.max(gap, Collections.min(now) - Collections.max(last));
                }
                last = now;
            }
        }
        return gap;
    }
}
```
