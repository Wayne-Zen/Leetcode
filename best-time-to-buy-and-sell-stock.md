[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)


```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        int maxGap = 0;
        int minVal = prices[0];
        for (int i = 1; i < prices.length; i++) {
            int newGap = prices[i] - minVal;
            if (newGap > maxGap) {
                maxGap = newGap;
            }
            if (prices[i] < minVal) {
                minVal = prices[i];
            }
        }
        return maxGap;
    }
}
```
