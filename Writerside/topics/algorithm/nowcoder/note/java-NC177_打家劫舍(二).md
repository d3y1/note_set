# java-NC177 打家劫舍(二)


    import java.util.*;
    
    /**
     * NC177 打家劫舍(二)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型一维数组
         * @return int整型
         */
        public int rob (int[] nums) {
            return solution1(nums);
            // return solution2(nums);
            // return solution3(nums);
        }
    
        /**
         * 动态规划
         *
         * dp[i][0]表示第i家不偷时前i家的最多偷窃金额
         * dp[i][1]表示第i家要偷时前i家的最多偷窃金额
         *
         * dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1]);
         * dp[i][1] = dp[i-1][0] + nums[i-1];
         *
         * @param nums
         * @return
         */
        private int solution1(int[] nums){
            int n = nums.length;
            if(n == 1){
                return nums[0];
            }
    
            int[][] dp = new int[n+1][2];
    
            int result;
    
            // 不偷第一家 最后一家偷或不偷都行
            dp[1][1] = 0;
            for(int i=2; i<=n; i++){
                dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1]);
                dp[i][1] = dp[i-1][0] + nums[i-1];
            }
            result = Math.max(dp[n][0], dp[n][1]);
    
            // 偷了第一家 最后一家不能偷
            dp[1][1] = nums[0];
            for(int i=2; i<=n; i++){
                dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1]);
                dp[i][1] = dp[i-1][0] + nums[i-1];
            }
            result = Math.max(result, dp[n][0]);
    
            return result;
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示前i家的最多偷窃金额
         *
         * dp[i] = Math.max(dp[i-1], dp[i-2]+nums[i-1])
         *
         * @param nums
         * @return
         */
        private int solution2(int[] nums){
            int n = nums.length;
            if(n == 1){
                return nums[0];
            }
    
            int[] dp = new int[n+1];
    
            int result;
    
            // 不偷第一家 最后一家偷或不偷都行
            dp[1] = 0;
            for(int i=2; i<=n; i++){
                dp[i] = Math.max(dp[i-1], dp[i-2]+nums[i-1]);
            }
            result = dp[n];
    
            // 偷了第一家 最后一家不能偷
            dp[1] = nums[0];
            for(int i=2; i<=n-1; i++){
                dp[i] = Math.max(dp[i-1], dp[i-2]+nums[i-1]);
            }
            result = Math.max(result, dp[n-1]);
    
            return result;
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示前i家的最多偷窃金额
         *
         * dp[i] = Math.max(dp[i-1], dp[i-2]+nums[i-1])
         *
         * @param nums
         * @return
         */
        private int solution3(int[] nums){
            int n = nums.length;
            if(n == 1){
                return nums[0];
            }
    
            int[] dp1 = new int[n+1];
            int[] dp2 = new int[n+1];
    
            int result;
    
            // 不偷第一家 最后一家偷或不偷都行
            dp1[1] = 0;
            // 偷了第一家 最后一家不能偷
            dp2[1] = nums[0];
            for(int i=2; i<=n; i++){
                dp1[i] = Math.max(dp1[i-1], dp1[i-2]+nums[i-1]);
                dp2[i] = Math.max(dp2[i-1], dp2[i-2]+nums[i-1]);
            }
            result = Math.max(dp1[n], dp2[n-1]);
    
            return result;
        }
    }

  

