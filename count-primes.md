[Link](https://leetcode.com/problems/count-primes/)

```java
public class Solution {
    public int countPrimes(int n) {
        if (n <= 2) {
            return 0;
        }
        boolean[] isPrime = new boolean[n];
        Arrays.fill(isPrime, true);
        isPrime[0] = false;
        isPrime[1] = false;
        int res = 0;
        for (int i = 2; i < isPrime.length; i++) {
            if (isPrime[i]) {
                res++;
                int x = i + i;
                while (x < isPrime.length) {
                    isPrime[x] = false;
                    x += i;
                }
            }
        }
        return res;
    }
}
```
