[Link](https://leetcode.com/problems/powx-n/)

* x^n = x^(n/2)*x^(n/2)*x^(n%2)

```java
public class Solution {
    public double help(double x, int n) {
        if (n == 0)
            return 1;
 
        double v = help(x, n / 2);
 
        if (n % 2 == 0) {
            return v * v;
        } else {
            return v * v * x;
        }
    }
 
    public double myPow(double x, int n) {
        if (n < 0) {
            return 1 / help(x, -n);
        } else {
            return help(x, n);
        }
    }
}
```
