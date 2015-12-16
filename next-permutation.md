[Link](https://leetcode.com/problems/next-permutation/)

1. find dropNumber, (right to left, first decreasing number)
2. find changeNumber, (right to left, first number larger than dropNumber)
3. swap dropNumber changeNumber
4. sort region after origin dropNumber postion

![](img/Photos/next-permutation.png)

```java
public class Solution {
    public void nextPermutation(int[] nums) {
        int p1 = -1;
        for (int i = nums.length - 2; i >= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                p1 = i;
                break;
            } 
        }
        if (p1 == -1) {
            Arrays.sort(nums);
            return;
        }
        int p2 = -1;
        for (int i = nums.length - 1; i >= 0; i--) {
            if (nums[i] > nums[p1]) {
                p2 = i;
                break;
            }
        }
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
        Arrays.sort(nums, p1 + 1, nums.length);
    }
}
```
