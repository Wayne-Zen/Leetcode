[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int N = prices.length;
        int[] sell = new int[N];
        int[] buy = new int[N];
        // 初始化是关键
        sell[0] = 0;
        sell[1] = Math.max(0, prices[1] - prices[0]);
        buy[0] = -prices[0];
        buy[1] = Math.max(-prices[0], -prices[1]);
        // 第i天买，卖，兜里的钱
        for (int i = 2; i < N; i++) {
            sell[i] = Math.max(sell[i - 1], buy[i - 1] + prices[i]); // 不卖, 卖 
            buy[i] = Math.max(buy[i - 1], sell[i - 2] - prices[i]); // 不买，买
        }
        return sell[sell.length - 1];
    }
}
```
