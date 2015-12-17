[Link](https://leetcode.com/problems/bitwise-and-of-numbers-range/)

* 数的左边共同的部分

```java
public class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        int mask = ~0;
        while ((m & mask) != (n & mask)) {
            mask <<= 1;
        }
        return m & mask;
    }
}
```
