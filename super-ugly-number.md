[Link](https://leetcode.com/problems/super-ugly-number/)

```java
public class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int[] indexes = new int[primes.length];
        int[] res = new int[n];
        res[0] = 1;
        int cnt = 1;
        while (cnt < n) {
            cnt++;
            int min = Integer.MAX_VALUE;
            for (int i = 0; i < primes.length; i++) {
                min = Math.min(min, primes[i] * res[indexes[i]]);
            }
            res[cnt - 1] = min;
            for (int i = 0; i < primes.length; i++) {
                if (min == primes[i] * res[indexes[i]]) {
                    indexes[i]++;
                }
            }
        }
        return res[n - 1];
    }
}
```
