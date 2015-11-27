[Link](https://leetcode.com/problems/single-number-ii/)

```java
public class Solution {
    public int singleNumber(int[] nums) {
        int[] bits = new int[32];
        for (int num : nums) {
            for (int i = 0; i < 32; i++) {
                bits[i] += (num >> i) & 1;
            }
        }
        int res = 0;
        int base = 1;
        for (int i = 0; i < 32; i++) {
            res += bits[i] % 3 * base;
            base *= 2;
        }
        return res;
    }
}
```
