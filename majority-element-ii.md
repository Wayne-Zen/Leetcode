[Link](https://leetcode.com/problems/majority-element-ii/)

```java
public class Solution {
    public List<Integer> majorityElement(int[] nums) {
        List<Integer> res = new ArrayList<Integer>();
        if (nums == null || nums.length == 0) {
            return res;
        }
        int val1 = 0;
        int cnt1 = 0;
        int val2 = 0;
        int cnt2 = 0;
        for (int num : nums) {
            if (cnt1 == 0) {
                val1 = num;
                cnt1++;
                continue;
            } else if (num == val1) {
                cnt1++;
                continue;
            }
            if (cnt2 == 0) {
                val2 = num;
                cnt2++;
                continue;
            } else if (num == val2) {
                cnt2++;
                continue;
            } 
            cnt1--;
            cnt2--;
        }
        if (val1 == val2) {
            res.add(val1);
            return res;
        }
        cnt1 = 0;
        cnt2 = 0;
        for (int num : nums) {
            if (num == val1) {
                cnt1++;
            } 
            if (num == val2) {
                cnt2++;
            }
        }
        if (cnt1 > nums.length / 3) {
            res.add(val1);
        }
        if (cnt2 > nums.length / 3) {
            res.add(val2);
        }
        return res;
    }
}
```
