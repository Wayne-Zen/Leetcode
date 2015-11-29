[Link](https://leetcode.com/problems/missing-number/)

```java
public class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        return (1 + n) * n / 2 - sum;
    }
}
```
