#### 题目：给出每天的股票价格，最多只有两次买入卖出的机会，并且如果手上有股票则不能再次购买，只能卖出后才能再次购买，问可以得到的最大收益是多少？

#### 思路：假设开始我一毛钱都没有，第一次买入后我的收益为buy1（此时收益为负），第一次卖出后我的收益记为sell1，第二次买入后我的收益记为buy2，第二次卖出后我的收益记为sell2。所以sell2便是最终最大的获得收益。
代码：
```
public class Solution {
    public int maxProfit(int[] prices) {
        int buy1 = Integer.MIN_VALUE, sell1 = 0, buy2 = Integer.MIN_VALUE, sell2 = 0;
        for(int price : prices) {
            buy1 = Math.max(buy1, -price);
            sell1 = Math.max(sell1, price + buy1);
            buy2 = Math.max(buy2, sell1 - price);
            sell2 = Math.max(sell2, price + buy2);
        }
        return sell2;
    }
}
```
