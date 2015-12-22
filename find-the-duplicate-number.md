[Link](https://leetcode.com/problems/find-the-duplicate-number/)

* O(nlogn) 

```java
public class Solution {
    public int findDuplicate(int[] nums) {
        int lo = 1;
        int hi = nums.length - 1;
        while (lo + 1 < hi) {
            int val = lo + (hi - lo) / 2;
            int less = less(nums, val);
            if (less < val) {
                lo = val;
            } else {
                hi = val;
            }
        }
        if (less(nums, hi) < hi) {
            return hi;
        } else {
            return lo;
        }
    }
    private int less(int[] nums, int pivotVal) {
        int less = 0;
        for (int num : nums) {
            if (num < pivotVal) {
                less++;
            } 
        }
        return less;
    }
}
```

* O(n)

```java
public class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0;
        int fast = 0;
        // 找到快慢指针相遇的地方
        while (true) {
            slow = nums[slow];
            fast = nums[nums[fast]];
            if (slow == fast) {
                break;
            }
        } 
        int find = 0;
        // 用一个新指针从头开始，直到和慢指针相遇
        while(find != slow){
            slow = nums[slow];
            find = nums[find];
        }
        return find;
    }
}
```
