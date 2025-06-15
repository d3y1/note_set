# java-JD4 上台阶


    import java.util.*;
    
    /**
     * JD4 上台阶
     * @author d3y1
     */
    public class GoUpstairs {
        private static final int MOD = 1000000007;
    
        /**
         * 动态规划
         *
         * dp[i]表示到达第i级的走法数
         * 
         * 举例子找规律
         * dp[i] = dp[i-1] + dp[i-2]
         *
         * @param n
         * @return
         */
        public int countWays(int n) {
            if(n == 1){
                return 0;
            }
            
            int[] dp = new int[n+1];
            dp[1] = 1;
            dp[2] = 1;
            for(int i=3; i<=n; i++){
                dp[i] = (dp[i-1] + dp[i-2])%MOD;
            }
    
            return dp[n];
        }
    }

  

