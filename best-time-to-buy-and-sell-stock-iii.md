[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int res = 0;
        if (prices.length == 0) {
            return 0;
        }
        int N = prices.length;
        int[] max1 = new int[N];
        int[] max2 = new int[N];
        int min = prices[0];
        for (int i = 1; i < N; i++) {
            max1[i] = Math.max(max1[i - 1], prices[i] - min);
            min = Math.min(min, prices[i]);
        }
        int max = prices[N - 1];
        for (int i = N - 2; i >= 0; i--) {
            max2[i] = Math.max(max2[i + 1], max - prices[i]);
            max = Math.max(max, prices[i]);
        }
        for (int i = 0; i < N; i++) {
            res = Math.max(res, max1[i] + max2[i]);
        }
        return res;
    }
}
```
