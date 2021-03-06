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
    private int transform(int x, int n) {
        return (2 * x + 1) % (n | 1);
    }
    public void wiggleSort(int[] nums) {
        // find median smaller | larger
        int median = find(nums, nums.length / 2);
        int lo = 0; 
        int hi = nums.length - 1;
        int n = nums.length;
        // wiggle sort larger | smaller
        for (int i = lo; i <= hi; i++) {
            if (nums[transform(i, n)] > median) {
                swap(nums, transform(lo, n), transform(i, n));
                lo++;
            } else if (nums[transform(i, n)] < median) {
                swap(nums, transform(hi, n), transform(i, n));
                hi--;
                i--;
            }
        }
        
    }
}
```
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
        if (nums == null || nums.length == 0) {
            return;
        }
        int median = find(nums, nums.length / 2);
        int lo = 0; 
        int hi = nums.length - 1;
        for (int i = lo; i <= hi; i++) {
            if (nums[i] > median) {
                swap(nums, i, lo++);
            } else if (nums[i] < median) {
                swap(nums, i, hi--);
                i--;
            }
        }
        
        int n = nums.length;
        int[] temp = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            temp[(2 * i + 1) % (n | 1)] = nums[i];
        }
        for (int i = 0; i < nums.length; i++) {
            nums[i] = temp[i];
        }
    }
}
```
