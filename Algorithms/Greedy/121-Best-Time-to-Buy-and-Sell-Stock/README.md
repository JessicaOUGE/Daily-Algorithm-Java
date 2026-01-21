# 121. Best Time to Buy and Sell Stock (Java)

**题目链接：** [LeetCode 121 - Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

---

## 💡 核心领悟 (Insights)
- **低买高卖**：我们的目标是找到一对 $(buy, sell)$，使得 $prices[sell] - prices[buy]$ 最大，且 $buy < sell$。
- **贪心策略**：在遍历数组的过程中，我们只需要记住**到目前为止的最低价格**（`minPrice`）。
- **同步更新**：每遇到一个新的价格，我们做两件事：
  1. 更新历史最低价。
  2. 计算如果今天卖出能赚多少钱，并更新历史最高利润（`maxProfit`）。
- **时机意识**：这道题不能在今天买入的同时卖出，且不能在买入之前卖出（时间轴不可逆）。

## 🚀 解题代码 (One Pass Approach)
```java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;
        
        for (int price : prices) {
            if (price < minPrice) {
                // 找到更低的买入点
                minPrice = price;
            } else if (price - minPrice > maxProfit) {
                // 如果今天卖出利润更高，更新它
                maxProfit = price - minPrice;
            }
        }
        return maxProfit;
    }
}
