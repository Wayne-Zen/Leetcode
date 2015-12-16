[Link](https://leetcode.com/problems/first-missing-positive/)

* [1,2,3,4,5]; nums[i] - 1 == i

```java
public class Solution {
    public int firstMissingPositive(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            while (nums[i] - 1 >= 0 // stop if current value is non-positive
                   && nums[i] - 1 < nums.length // current must be positive, but may out of index bound
                   && nums[i] - 1 != i // swap index are the same
                   && nums[nums[i] - 1] != nums[i]) { // swap value are the same
                swap(nums, i, nums[i] - 1);
            }
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] - 1 != i) {
                return i + 1;
            }
        }
        return nums.length + 1;
    }
    
    private void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp;
    }
}
```
