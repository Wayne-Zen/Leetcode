[Link](https://leetcode.com/problems/product-of-array-except-self/)

```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] f = new int[nums.length];
        f[0] = 1;
        for (int i = 1; i < f.length; i++) {
            f[i] = f[i - 1] * nums[i - 1];
        }
        int[] r = new int[nums.length];
        r[r.length - 1] = 1;
        for (int i = r.length - 2; i >= 0; i--) {
            r[i] = r[i + 1] * nums[i + 1];
        }
        int[] res = new int[nums.length];
        for (int i = 0; i < res.length; i++) {
            res[i] = f[i] * r[i];
        }
        return res;
    }
}
```
