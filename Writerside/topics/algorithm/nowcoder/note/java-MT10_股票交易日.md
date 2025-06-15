# java-MT10 股票交易日


    import java.util.*;
    
    public class Stock {
        public int maxProfit(int[] prices, int n) {
            return solution1(prices, n);
            // return solution2(prices, n);
            // return solution3(prices, n);
        }
    
        /**
         * 动态规划: 状态机
         *
         * 两次交易同时开始
         *
         * dp[i][0]表示股票前i种价格第一次交易买入后所得收益
         * dp[i][1]表示股票前i种价格第一次交易卖出后所得收益
         * dp[i][2]表示股票前i种价格第二次交易买入后所得收益
         * dp[i][3]表示股票前i种价格第二次交易卖出后所得收益
         *
         * 四种状态:
         * 第一次交易买入: 要么是之前买的, 要么是今天买的
         * 第一次交易卖出: 要么是之前卖的, 要么是今天卖的
         * 第二次交易买入: 要么是之前买的, 要么是今天买的
         * 第二次交易卖出: 要么是之前卖的, 要么是今天卖的
         *
         * 分别对应关系式:
         * dp[i][0] = max(dp[i-1][0], -prices[i])
         * dp[i][1] = max(dp[i-1][1], dp[i-1][0]+prices[i])
         * dp[i][2] = max(dp[i-1][2], dp[i-1][1]-prices[i])
         * dp[i][3] = max(dp[i-1][3], dp[i-1][2]+prices[i])
         *
         * @param prices
         * @param n
         * @return
         */
        private int solution1(int[] prices, int n){
            int[][] dp = new int[n][4];
    
            // 一次买入
            dp[0][0] = -prices[0];
            // 一次卖出
            dp[0][1] = 0;
            // 二次买入
            dp[0][2] = -prices[0];
            // 二次卖出
            dp[0][3] = 0;
            for(int i=1; i<n; i++){
                dp[i][0] = Math.max(dp[i-1][0], -prices[i]);
                dp[i][1] = Math.max(dp[i-1][1], dp[i-1][0]+prices[i]);
                dp[i][2] = Math.max(dp[i-1][2], dp[i-1][1]-prices[i]);
                dp[i][3] = Math.max(dp[i-1][3], dp[i-1][2]+prices[i]);
            }
    
            return dp[n-1][3];
        }
    
        /**
         * 动态规划: 状态机
         *
         * 两次交易同时开始
         *
         * buy1 表示股票前i种价格第一次交易买入后所得收益
         * sell1 表示股票前i种价格第一次交易卖出后所得收益
         * buy2 表示股票前i种价格第二次交易买入后所得收益
         * sell2 表示股票前i种价格第二次交易卖出后所得收益
         *
         * 四种状态:
         * 第一次交易买入: 要么是之前买的, 要么是今天买的
         * 第一次交易卖出: 要么是之前卖的, 要么是今天卖的
         * 第二次交易买入: 要么是之前买的, 要么是今天买的
         * 第二次交易卖出: 要么是之前卖的, 要么是今天卖的
         *
         * 分别对应关系式:
         * buy1 = max(buy1, -prices[i])
         * sell1 = max(sell1, buy1+prices[i])
         * buy2 = max(buy2, sell1-prices[i])
         * sell2 = max(sell2, buy2+prices[i])
         *
         * @param prices
         * @param n
         * @return
         */
        private int solution2(int[] prices, int n){
            // 一次买入
            int buy1 = -prices[0];
            // 一次卖出
            int sell1 = 0;
            // 二次买入
            int buy2 = -prices[0];
            // 二次卖出
            int sell2 = 0;
            for(int i=1; i<n; i++){
                buy1 = Math.max(buy1, -prices[i]);
                sell1 = Math.max(sell1, buy1+prices[i]);
                buy2 = Math.max(buy2, sell1-prices[i]);
                sell2 = Math.max(sell2, buy2+prices[i]);
            }
    
            return sell2;
        }
    
        /**
         * 动态规划: 双向
         * @param prices
         * @param n
         * @return
         */
        private int solution3(int[] prices, int n){
            int[] left = new int[n];
            int[] right = new int[n];
            int leftMin = prices[0];
            int rightMax = prices[n-1];
            int sum = 0;
            
            // 左段一次交易最大收益
            for(int i=1; i<n; i++){
                leftMin = Math.min(prices[i], leftMin);
                left[i] = Math.max(prices[i]-leftMin, left[i-1]);
            }
            // 右段一次交易最大收益
            for(int i=n-2 ; i>=0; i--){
                rightMax = Math.max(prices[i], rightMax);
                right[i] = Math.max(rightMax-prices[i], right[i+1]);
            }
            // 两次交易最大收益
            for(int i=0 ; i<n; i++){
                sum = Math.max(sum, left[i]+right[i]);
            }
    
            return sum;
        }
    }

  

