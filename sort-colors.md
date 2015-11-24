[Link](https://leetcode.com/problems/sort-colors/)

* for (int i = lo; i <= hi; i++)// <= hi

```java
public class Solution {
    public void sortColors(int[] nums) {
        int lo = 0;
        int hi = nums.length - 1;
        for (int i = lo; i <= hi; i++) {
            if (nums[i] == 0) {
                swap(nums, lo, i);
                lo++;
            } else if (nums[i] == 2) {
                swap(nums, hi, i);
                hi--;
                i--;
            }
        }
    }
    
    private void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp; 
    }
}
```
