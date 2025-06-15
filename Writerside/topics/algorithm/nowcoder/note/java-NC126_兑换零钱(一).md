# java-NC126 兑换零钱(一)


    import java.util.*;
    
    /**
     * NC126 兑换零钱(一)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 最少货币数
         * @param arr int整型一维数组 the array
         * @param aim int整型 the target
         * @return int整型
         */
        public int minMoney (int[] arr, int aim) {
            return solution(arr, aim);
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示组成目标钱数i时需要的最少货币数
         *
         * dp[i] = Math.min(dp[i], dp[i-coins[j]]+1)  , (i >= arr[j])
         *
         * @param arr
         * @param aim
         * @return
         */
        private static int solution(int[] arr, int aim){
            if(aim == 0){
                return 0;
            }
    
            int[] dp = new int[aim+1];
            int len = arr.length;
            for(int i=1; i<=aim; i++){
                dp[i] = Integer.MAX_VALUE;
                for(int j=0; j<len; j++){
                    if(i >= arr[j]){
                        // dp[i-arr[j]]可用货币组成
                        if(dp[i-arr[j]] != Integer.MAX_VALUE){
                            dp[i] = Math.min(dp[i], dp[i-arr[j]]+1);
                        }
                    }
                }
            }
    
            return dp[aim]==Integer.MAX_VALUE ? -1 : dp[aim];
        }
    }

  

