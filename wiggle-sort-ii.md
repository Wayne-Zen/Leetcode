[Link](https://leetcode.com/problems/wiggle-sort-ii/)

```java
public class Solution {
    private int find(int[] nums, int index) {
        int lo = 0;
        int hi = nums.length - 1;
        while (true) {
            int pos = partition(nums, lo, hi);
            if (pos == index) {
                return nums[pos];
            } else if (pos < index) {
                lo = pos + 1;
            } else {
                hi = pos - 1;
            }
        }
    }
    private int partition(int[] nums, int lo, int hi) {
        for (int i = lo; i < hi; i++) {
            if (nums[i] < nums[hi]) {
                swap(nums, i, lo++);
            }
        }
        swap(nums, lo, hi);
        return lo;
    }
    private void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp;
    }
    public void wiggleSort(int[] nums) {
        int median = find(nums, nums.length / 2);
        int lo = 0; 
        int hi = nums.length - 1;
        for (int i = lo; i <= hi; i++) {
            if (nums[i] < median) {
                swap(nums, lo++, i);
            } else if (nums[i] > median) {
                swap(nums, hi--, i--);
            }
        }
        
        int[] res = new int[nums.length];
        int i1 = (nums.length - 1) / 2;
        int i2 = nums.length - 1;
        for (int i = 0; i < res.length; i++) {
            if (i % 2 == 0) {
                res[i] = nums[i1--];
            } else {
                res[i] = nums[i2--];
            }
        }
        for (int i = 0; i < res.length; i++) {
            nums[i] = res[i];
        }
    }
}
```
