[Link](https://leetcode.com/problems/kth-largest-element-in-an-array/)

```java
public class Solution {
    public int findKthLargest(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            throw new IllegalArgumentException();
        }
        int lo = 0;
        int hi = nums.length - 1;
        while (true) {
            int p = partition(nums, lo, hi);
            //System.out.println(Arrays.toString(nums) + " " + p);
            if (p == k - 1) {
                return nums[p];
            } else if (p < k - 1) {
                lo = p + 1;
            } else {
                hi = p - 1;
            }
        }
    }
    private int partition(int[] nums, int lo, int hi) {
        int pivot = nums[lo];
        for (int i = lo; i <= hi; i++) {
            if (nums[i] > pivot) {
                swap(nums, lo, i);
                lo++;
            } else if (nums[i] < pivot) {
                swap(nums, hi, i);
                hi--;
                i--;
            }
        }
        return lo;
    }
    private void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp;
    }
    
}
```
