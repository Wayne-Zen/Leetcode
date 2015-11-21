[Link](https://leetcode.com/problems/reverse-integer/)

* 负数
* 头几位为0
* 溢出
* 注意Integer.MIN_VALUE的绝对值是比Integer.MAX_VALUE大1的，所以经常要单独处理

```java
public class Solution {
    public int reverse(int x) {
        if(x == Integer.MIN_VALUE) {
            return 0;
        }
        int neg = x < 0 ? -1 : 1;
        x = Math.abs(x);
        int res = 0;
        while (x > 0) {
            int digit = x % 10;
            x = x / 10;
            if (res > (Integer.MAX_VALUE - digit) / 10) {
                return 0;
            }
            res = res * 10 + digit;
        }
        return res * neg;
    }
}
```
