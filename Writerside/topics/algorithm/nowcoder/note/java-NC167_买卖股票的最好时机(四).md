# java-NC167 买卖股票的最好时机(四)

```java
import java.util.*;

/**
 * NC167 买卖股票的最好时机(四)
 * @author d3y1
 */
public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     *
     * @param prices int整型一维数组
     * @param k int整型
     * @return int整型
     */
    public int maxProfit (int[] prices, int k) {
        // return solution1(prices, k);
        return solution2(prices, k);
        // return solution3(prices, k);
        // return solution4(prices, k);
        // return solution5(prices, k);
    }

    /**
     * 动态规划: 状态机
     *
     * dp[i][1]表示股票前i天价格第一次交易买入后所得收益
     * dp[i][2]表示股票前i天价格第一次交易卖出后所得收益
     * dp[i][3]表示股票前i天价格第二次交易买入后所得收益
     * dp[i][4]表示股票前i天价格第二次交易卖出后所得收益
     * ...
     * dp[i][2k-1]表示股票前i天价格第k次交易卖出后所得收益
     * dp[i][2k]  表示股票前i天价格第k次交易卖出后所得收益
     *
     * 2k种状态:
     * 第一次交易买入: 要么是之前买的, 要么是今天买的
     * 第一次交易卖出: 要么是之前卖的, 要么是今天卖的
     * 第二次交易买入: 要么是之前买的, 要么是今天买的
     * 第二次交易卖出: 要么是之前卖的, 要么是今天卖的
     * ...
     * 第k次交易买入: 要么是之前买的, 要么是今天买的
     * 第k次交易卖出: 要么是之前卖的, 要么是今天卖的
     *
     * 关系式:
     *            { Math.max(dp[i-1][j], dp[i-1][j-1]-prices[i-1])  , j%2 == 1
     * dp[i][j] = {
     *            { Math.max(dp[i-1][j], dp[i-1][j-1]+prices[i-1])  , j%2 == 0
     *
     * @param prices
     * @param k
     * @return
     */
    private int solution1(int[] prices, int k){
        int n = prices.length;
        k = Math.min(k, n/2);

        int[][] dp = new int[n+1][2*k+1];

        // init
        for(int j=1; j<2*k+1; j++){
            if(j%2 == 1){
                dp[1][j] = -prices[0];
            }else{
                dp[1][j] = 0;
            }
        }

        for(int i=2; i<=n; i++){
            for(int j=1; j<2*k+1; j++){
                if(j%2 == 1){
                    dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-1]-prices[i-1]);
                }else{
                    dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-1]+prices[i-1]);
                }
            }
        }

        return dp[n][2*k];
    }

    /**
     * 动态规划: 三维数组
     *
     * dp[i][j][0]表示前i天股票价格交易j次(一买一卖)后手上未持股票时的最大收益
     * dp[i][j][1]表示前i天股票价格交易j次(一买一卖)后手上持有股票时的最大收益
     *
     * dp[i][j][0] = Math.max(dp[i-1][j][0], dp[i-1][j][1]+prices[i])    , 1<=i<n && 1<=j<=k
     * dp[i][j][1] = Math.max(dp[i-1][j][1], dp[i-1][j-1][0]-prices[i])  , 1<=i<n && 1<=j<=k
     *
     * @param prices
     * @param k
     * @return
     */
    private int solution2(int[] prices, int k){
        int n = prices.length;
        k = Math.min(k, n/2);

        int[][][] dp = new int[n][k+1][2];

        // init
        for(int j=1; j<=k; j++){
            dp[0][j][0] = 0;
            dp[0][j][1] = -prices[0];
        }

        for(int i=1; i<n; i++){
            for(int j=1; j<=k; j++){
                // dp[i-1][j][1]+prices[i] -> 卖(次数不变, j -> j)
                dp[i][j][0] = Math.max(dp[i-1][j][0], dp[i-1][j][1]+prices[i]);
                // dp[i-1][j-1][0]-prices[i] -> 买(次数加1, j-1 -> j)
                dp[i][j][1] = Math.max(dp[i-1][j][1], dp[i-1][j-1][0]-prices[i]);
            }
        }

        return dp[n-1][k][0];
    }

    /**
     * 动态规划: 二维数组
     *
     * sell[i][j]表示前i天股票价格交易j次(一买一卖)后手上未持股票时的最大收益
     * buy[i][j]表示前i天股票价格交易j次(一买一卖)后手上持有股票时的最大收益
     *
     * sell[i][j] = Math.max(sell[i-1][j], buy[i-1][j]+prices[i])   , 1<=i<n && 1<=j<=k
     * buy[i][j] = Math.max(buy[i-1][j], sell[i-1][j-1]-prices[i])  , 1<=i<n && 1<=j<=k
     *
     * @param prices
     * @param k
     * @return
     */
    private int solution3(int[] prices, int k){
        int n = prices.length;
        k = Math.min(k, n/2);

        int[][] sell = new int[n][k+1];
        int[][] buy = new int[n][k+1];

        // init
        for(int j=1; j<=k; j++){
            sell[0][j] = 0;
            buy[0][j] = -prices[0];
        }

        for(int i=1; i<n; i++){
            for(int j=1; j<=k; j++){
                // buy[i-1][j]+prices[i] -> 卖(次数不变, j -> j)
                sell[i][j] = Math.max(sell[i-1][j], buy[i-1][j]+prices[i]);
                // sell[i-1][j-1]-prices[i] -> 买(次数加1, j-1 -> j)
                buy[i][j] = Math.max(buy[i-1][j], sell[i-1][j-1]-prices[i]);
            }
        }

        return sell[n-1][k];
    }

    /**
     * 动态规划: 一维数组(空间压缩)
     *
     * sell[j]表示交易j次(一买一卖)后手上未持股票时的最大收益
     * buy[j]表示交易j次(一买一卖)后手上持有股票时的最大收益
     *
     * sell[j] = Math.max(sell[j], buy[j]+prices[i])   , 1<=i<n && 1<=j<=k
     * buy[j] = Math.max(buy[j], sell[j-1]-prices[i])  , 1<=i<n && 1<=j<=k
     *
     * @param prices
     * @param k
     * @return
     */
    private int solution4(int[] prices, int k){
        int n = prices.length;
        k = Math.min(k, n/2);

        int[] buy = new int[k+1];
        int[] sell = new int[k+1];

        // init
        for(int j=1; j<=k; j++){
            sell[j] = 0;
            buy[j] = -prices[0];
        }

        for(int i=1; i<n; i++){
            for(int j=1; j<=k; j++){
                sell[j] = Math.max(sell[j], buy[j]+prices[i]);
                // 此处 sell[j-1] = sell[i][j-1](实际需要的sell[i-1][j-1]已被覆盖, 但是不影响最终结果)

                //    sell[i][j] = Math.max(sell[i-1][j], buy[i-1][j]+prices[i])
                // => sell[i][j-1] = Math.max(sell[i-1][j-1], buy[i-1][j-1]+prices[i])
                // => sell[j-1] = Math.max(sell[i-1][j-1], buy[i-1][j-1]+prices[i])
                // => sell[j-1]-prices[i] = Math.max(sell[i-1][j-1]-prices[i], buy[i-1][j-1]+prices[i]-prices[i])
                //                        = Math.max(sell[i-1][j-1]-prices[i], buy[i-1][j-1])
                // buy[j] = Math.max(buy[j], sell[j-1]-prices[i])
                //        = Math.max(buy[i-1][j], sell[j-1]-prices[i])
                //        = Math.max(buy[i-1][j], sell[i-1][j-1]-prices[i], buy[i-1][j-1])
                //        = Math.max(buy[i-1][j], sell[i-1][j-1]-prices[i]) [buy[i-1][j] >= buy[i-1][j-1]]
                // 可见, 与solution3中二维数组关系式是相同的
                buy[j] = Math.max(buy[j], sell[j-1]-prices[i]);
            }
        }

        return sell[k];
    }

    /**
     * 动态规划
     *
     * dp[j]表示前j天股票价格某次交易后的最大收益
     *
     *         { Math.max(maxProfit, dp[j]-prices[j])  , 买入
     * dp[j] = {
     *         { Math.max(maxProfit, dp[j]+prices[j])  , 卖出
     *
     * @param prices
     * @param k
     * @return
     */
    private int solution5(int[] prices, int k){
        int n = prices.length;
        k = Math.min(k, n/2);

        int[] dp = new int[n];

        int maxProfit;
        for(int i=1; i<=k; i++){
            // 买入
            maxProfit = Integer.MIN_VALUE;
            for(int j=0; j<n; j++){
                dp[j] = Math.max(maxProfit, dp[j]-prices[j]);
                maxProfit = Math.max(maxProfit, dp[j]);
            }

            // 卖出
            maxProfit = Integer.MIN_VALUE;
            for(int j=0; j<n; j++){
                dp[j] = Math.max(maxProfit, dp[j]+prices[j]);
                maxProfit = Math.max(maxProfit, dp[j]);
            }
        }

        return dp[n-1];
    }
}
```
