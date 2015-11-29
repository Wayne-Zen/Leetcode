[Link](https://leetcode.com/problems/single-number-iii/)

```java
public class Solution {
    public int[] singleNumber(int[] nums) {
        int xor = 0;
        for (int num : nums) {
            xor = xor ^ num;
        }
        //找分离位
        int index = 0;
        for (int i = 0; i < 32; i++) {
            if (((xor >> i) & 1) == 1) {
                index = i;
                break;
            }
        }
        // group
        int v1 = 0;
        int v2 = 0;
        for (int num : nums) {
            if (((num >> index) & 1) == 1) {
                v1 = v1 ^ num;
            } else {
                v2 = v2 ^ num;
            }
        }
        return new int[]{v1, v2};
    }
}
```
