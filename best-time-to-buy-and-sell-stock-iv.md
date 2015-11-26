[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

* 传统的动态规划我们会这样想，到第i天时进行j次交易的最大收益，要么等于到第i-1天时进行j次交易的最大收益（第i天价格低于第i-1天的价格），要么等于到第i-1天时进行j-1次交易，然后第i天进行一次交易（第i天价格高于第i-1天价格时）。于是得到动规方程如下（其中diff = prices[i] – prices[i – 1]）

> profit[i][j] = max(profit[i – 1][j], profit[i – 1][j – 1] + diff)

* 因为diff是第i天和第i-1天的差额收益，如果第i-1天当天本身也有交易呢（也就是说第i-1天刚卖出了股票，然后又买入等到第i天再卖出），那么这两次交易就可以合为一次交易，这样profit[i – 1][j – 1] + diff实际上只进行了j-1次交易，而不是最多可以的j次，这样得到的最大收益就小了。

* 用local[i][j]表示到达第i天时，最多进行j次交易的局部最优解；用global[i][j]表示到达第i天时，最多进行j次的全局最优解。它们二者的关系如下（其中diff = prices[i] – prices[i – 1]）

> local[i][j] = max(global[i – 1][j – 1] , local[i – 1][j] + diff)  
global[i][j] = max(global[i – 1][j], local[i][j])

* local[i][j]和global[i][j]的区别是：local[i][j]意味着在第i天一定有交易（卖出）发生，当第i天的价格高于第i-1天（即diff > 0）时，那么可以把这次交易（第i-1天买入第i天卖出）跟第i-1天的交易（卖出）合并为一次交易，即local[i][j]=local[i-1][j]+diff；当第i天的价格不高于第i-1天（即diff<=0）时，那么local[i][j]=global[i-1][j-1]+diff，而由于diff<=0，所以可写成local[i][j]=global[i-1][j-1]。global[i][j]就是我们所求的前i天最多进行k次交易的最大收益，可分为两种情况：如果第i天没有交易（卖出），那么global[i][j]=global[i-1][j]；如果第i天有交易（卖出），那么global[i][j]=local[i][j]

* 当k大于天数时，其实就退化成 Best Time to Buy and Sell Stock II 了

```java
public class Solution {
    private int maxProfit2(int[] prices) {
        int res = 0;
        for (int i = 1; i < prices.length; i++) {
            res += Math.max(0, prices[i] - prices[i - 1]);
        }
        return res;
    }
    public int maxProfit(int k, int[] prices) {
        if (prices == null || prices.length == 0 || prices.length == 1) {
            return 0;
        }
        if (k >= prices.length) {
            return maxProfit2(prices);
        }
        int N = prices.length;
        int[][] local = new int[N][k + 1];
        int[][] global = new int[N][k + 1];
        
        for (int i = 1; i < N; i++) {
            int diff = prices[i] - prices[i - 1];
            for (int j = 1; j <= k; j++) {
                // local 的话，意味着第i天进行交易
                // 1. 第i天交易（local[i]），第i－1天也交易（local[i-1]），可以合并最后一笔交易
                //    即前i－1天允许进行j笔交易，而不是j-1笔
                // 2. 第i天交易（local[i]），第i－1天不一定交易（global[i-1]），只有j-1笔交易可以使用
                local[i][j] = Math.max(global[i - 1][j - 1], local[i - 1][j] + diff);
                // global 的话， 意味着第i天不一定进行交易
                // 1. 第i天交易，直接退化为local
                // 2. 第i天不交易，前i－1天还有j－1笔交易可以使用
                global[i][j] = Math.max(global[i - 1][j], local[i][j]);
            }
        }
        
        return global[N - 1][k];
    }
}
```
