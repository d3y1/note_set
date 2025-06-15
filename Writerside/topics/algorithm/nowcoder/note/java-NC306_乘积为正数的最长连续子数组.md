# java-NC306 乘积为正数的最长连续子数组


    import java.util.*;
    
    /**
     * NC306 乘积为正数的最长连续子数组
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型ArrayList
         * @return int整型
         */
        public int findLongestSubArray (ArrayList<Integer> nums) {
            return solution(nums);
        }
    
        /**
         * 动态规划
         *
         * dp[i][0]表示以数组中第i个整数为结尾的子数组的乘积为负数的最长长度
         * dp[i][1]表示以数组中第i个整数为结尾的子数组的乘积为正数的最长长度
         * 
         * num: 数组中第i个整数
         * 
         * 1. num>0时:
         *            { dp[i-1][0] + 1  , dp[i-1][0] > 0
         * dp[i][0] = {
         *            { 0               , dp[i-1][0] = 0
         * dp[i][1] = dp[i-1][1] + 1
         * 
         * 2. num<0时:
         * dp[i][0] = dp[i-1][1] + 1
         *            { dp[i-1][0] + 1  , dp[i-1][0] > 0
         * dp[i][1] = {
         *            { 0               , dp[i-1][0] = 0
         * 
         * 3. num=0时:
         * dp[i][0] = 0
         * dp[i][1] = 0
         * 
         * @param nums
         * @return
         */
        private int solution(ArrayList<Integer> nums){
            int n = nums.size();
    
            int[][] dp = new int[n+1][2];
    
            int num;
            int len = 0;
            for(int i=1; i<=n; i++){
                num = nums.get(i-1);
                if(num > 0){
                    if(dp[i-1][0] > 0){
                        dp[i][0] = dp[i-1][0] + 1;
                    }
                    dp[i][1] = dp[i-1][1] + 1;
                }
                if(num < 0){
                    dp[i][0] = dp[i-1][1] + 1;
                    if(dp[i-1][0] > 0){
                        dp[i][1] = dp[i-1][0] + 1;
                    }
                }
    
                len = Math.max(len, dp[i][1]);
            }
    
    
            return len;
        }
    }

  

