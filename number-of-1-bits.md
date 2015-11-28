[Link](https://leetcode.com/problems/number-of-1-bits/)

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int res = 0;
        for (int i = 0; i < 32; i++) {
            res += (n >> i) & 1;
        }
        return res;
    }
}
```
