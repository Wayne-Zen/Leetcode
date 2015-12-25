[Link](https://leetcode.com/problems/bitwise-and-of-numbers-range/)

* 数的左边共同的部分

```java
public class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        int i = 0;
        while (m != n) {
            m >>= 1;
            n >>= 1;
            i++;
        }
        return m << i;
    }
}
```
