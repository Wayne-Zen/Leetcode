[Link](https://leetcode.com/problems/majority-element-ii/)

```java
public class Solution {
    public List<Integer> majorityElement(int[] nums) {
        List<Integer> res = new ArrayList<Integer>();
        if (nums == null || nums.length == 0) {
            return res;
        }
        int can1 = 0;
        int can2 = 0;
        int cnt1 = 0;
        int cnt2 = 0;
        for (int x : nums) {
            if (cnt1 == 0) {
                can1 = x;
                cnt1 = 1;
                continue;
            } else if (x == can1) {
                cnt1++;
                continue;
            }
            if (cnt2 == 0) {
                can2 = x;
                cnt2 = 1;
                continue;
            } else if (x == can2) {
                cnt2++;
                continue;
            }
            if (x != can1 && x != can2) {
                cnt1--;
                cnt2--;
            }
        }
        
        if (can1 == can2) {
            res.add(can1);
            return res;
        }
        cnt1 = 0;
        cnt2 = 0;
        for (int x : nums) {
            if (x == can1) {
                cnt1++;
            }
            if (x == can2) {
                cnt2++;
            }
        }
        if (cnt1 > nums.length/3) {
            res.add(can1);
        }
        if (cnt2 > nums.length/3) {
            res.add(can2);
        }
        return res;
    }
}
```
