[Link](https://leetcode.com/problems/ugly-number-ii/)

* 不能用if－else
* 第n个，下标是n－1


```java
public class Solution {
    public int nthUglyNumber(int n) {
        int[] res = new int[n];
        res[0] = 1;
        int i2 = 0;
        int i3 = 0;
        int i5 = 0;
        for (int i = 1; i < n; i++) {
            res[i] = Math.min(Math.min(res[i2] * 2, res[i3] * 3), res[i5] * 5);
            if (res[i] == res[i2] * 2) {
                i2++;
            }
            if (res[i] == res[i3] * 3) {
                i3++;
            }
            if (res[i] == res[i5] * 5) {
                i5++;
            }
        }
        return res[n - 1];
    }
}
```
