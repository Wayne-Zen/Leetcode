[Link](https://leetcode.com/problems/range-sum-query-immutable/)

```java
public class NumArray {
    int[] running;
    
    public NumArray(int[] nums) {
        running = new int[nums.length + 1];
        running[0] = 0;
        for (int i = 0; i < nums.length; i++) {
            running[i + 1] = running[i] + nums[i];
        }
    }

    public int sumRange(int i, int j) {
        return running[j + 1] - running[i];
    }
}


// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.sumRange(1, 2);
```
