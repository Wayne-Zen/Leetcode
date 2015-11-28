[Link](https://leetcode.com/problems/power-of-two/)

```java
public class Solution {
    public boolean isPowerOfTwo(int n) {
        return (n > 0) && (n & (n - 1)) == 0;
    }
}
```
