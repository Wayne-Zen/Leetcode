[Link](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int lo = 0;
        int hi = numbers.length - 1;
        while (lo < hi) {
            if (numbers[lo] + numbers[hi] == target) {
                return new int[]{lo + 1, hi + 1};
            } else if (numbers[lo] + numbers[hi] < target) {
                lo++;
            } else {
                hi--;
            }
        }
        return new int[]{-1, -1};
    }
}
```
