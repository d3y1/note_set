# java-NC206 跳跃游戏(二)


    import java.util.*;
    
    /**
     * NC206 跳跃游戏(二)
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
        public int maxJumpGrade (int[] nums) {
            // return solution1(nums);
            return solution2(nums);
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示到达位置num[i]处所能获得的最多积分
         *
         * dp[j] = Math.max(dp[j],dp[i]+nums[j])  , i+1<=j<=Math.min(i+nums[i], n-1)
         *
         * @param nums
         * @return
         */
        private int solution1(int[] nums){
            int n = nums.length;
            if(n == 0){
                return -1;
            }
            if(n == 1){
                return nums[0];
            }
    
            int[] dp = new int[n];
            Arrays.fill(dp, -1);
            dp[0] = nums[0];
    
            for(int i=0; i<n; i++){
                // 当前位置不可达
                if(dp[i] == -1){
                    break;
                }
                for(int j=i+1; j<=Math.min(i+nums[i], n-1); j++){
                    dp[j] = Math.max(dp[j], dp[i]+nums[j]);
                }
            }
    
            return dp[n-1];
        }
    
        /**
         * 动态规划: 从后向前
         *
         * dp[i]表示从nums[i]位置跳到末尾所能获得的最多积分
         *
         * dp[i] = dp[pos] + nums[i]  , i+nums[i] >= pos
         *
         * @param nums
         * @return
         */
        private int solution2(int[] nums){
            int n = nums.length;
            if(n == 0){
                return -1;
            }
            if(n == 1){
                return nums[0];
            }
    
            int[] dp = new int[n];
            dp[n-1] = nums[n-1];
    
            // 能够跳到末尾的最小位置
            int pos = n-1;
            for(int i=n-2; i>=0; i--){
                if(i+nums[i] >= pos){
                    dp[i] = dp[pos] + nums[i];
                    pos = i;
                }
            }
    
            // 从开始处不能跳到末尾
            if(pos != 0){
                return -1;
            }
    
            return dp[0];
        }
    }

  

