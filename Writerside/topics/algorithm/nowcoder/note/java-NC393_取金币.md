# java-NC393 取金币


    import java.util.*;
    
    /**
     * NC393 取金币
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param coins int整型一维数组
         * @return int整型
         */
        public int getCoins (ArrayList<Integer> coins) {
            return solution(coins);
        }
    
        /**
         * 动态规划
         * 
         * 相似 -> NC326 能量项链
         *
         * dp[i][j]表示区间[i,j]能得到的最多积分
         * 
         *            { Math.max(dp[i][j], dp[k+1][j]+coins[i-1]*coins[k]*coins[j+1])             , k=i   && 1<=i<=j<=n
         * dp[i][j] = { Math.max(dp[i][j], dp[i][k-1]+coins[i-1]*coins[k]*coins[j+1])             , k=j   && 1<=i<=j<=n
         *            { Math.max(dp[i][j], dp[i][k-1]+dp[k+1][j]+coins[i-1]*coins[k]*coins[j+1])  , i<k<j && 1<=i<=j<=n
         *
         * @param coinList
         * @return
         */
        private int solution(ArrayList<Integer> coinList){
            int n = coinList.size();
            int[] coins = new int[n+2];
            for(int i=0; i<n; i++){
                coins[i+1] = coinList.get(i);
            }
            coins[0] = 1;
            coins[n+1] = 1;
    
            int[][] dp = new int[n+2][n+2];
    
            // 滑动窗口
            for(int gap=0; gap<n; gap++){
                // 区间[i,j]能得到的最多积分
                for(int i=1,j=i+gap; j<=n; i++,j++){
                    // [i,k-1] k [k+1,j] <- k:区间[i,j]最后选择金币位置索引
                    for(int k=i; k<=j; k++){
                        // 最后选左边界
                        if(k == i){
                            dp[i][j] = Math.max(dp[i][j], dp[k+1][j]+coins[i-1]*coins[k]*coins[j+1]);
                        }
                        // 最后选右边界
                        else if(k == j){
                            dp[i][j] = Math.max(dp[i][j], dp[i][k-1]+coins[i-1]*coins[k]*coins[j+1]);
                        }
                        // 最后选区间中间
                        else{
                            dp[i][j] = Math.max(dp[i][j], dp[i][k-1]+dp[k+1][j]+coins[i-1]*coins[k]*coins[j+1]);
                        }
                    }
                }
            }
    
            return dp[1][n];
        }
    }

  

