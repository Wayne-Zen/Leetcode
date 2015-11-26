[Link](https://leetcode.com/problems/longest-consecutive-sequence/)

```java
public class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        HashSet<Integer> set = new HashSet<Integer>();
        for (int n : nums) {
            set.add(n);
        }
        int max = 0;
        for (int n : nums) {
            if (!set.contains(n)) {
                continue;
            }
            int len = 1;
            int n1 = n - 1;
            int n2 = n + 1;
            while (set.contains(n1) || set.contains(n2)) {
                if (set.contains(n1)) {
                    len++;
                    set.remove(n1);
                    n1--;
                }
                if (set.contains(n2)) {
                    len++;
                    set.remove(n2);
                    n2++;
                }
            }
            max = Math.max(max, len);
        }
        return max;
    }
}
```
