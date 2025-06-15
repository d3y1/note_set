# java-NC155 最长严格上升子数组(一)


    import java.util.*;
    
    /**
     * NC155 最长严格上升子数组(一)
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
        public int maxSubArrayLengthTwo (int[] nums) {
            return solution(nums);
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示以第i个元素为结尾(nums[i]必选)的子数组的最长严格上升长度
         *
         * dp[i] = dp[i-1]+1  , (nums[i] > nums[i-1])
         *
         * @param nums
         * @return
         */
        private int solution(int[] nums){
            int n = nums.length;
            if(n <= 2){
                return n;
            }
    
            // 初始化
            int[] dp = new int[n];
            Arrays.fill(dp, 1);
    
            int result = 1;
            for(int i=1; i<n; i++){
                if(nums[i] > nums[i-1]){
                    dp[i] = dp[i-1]+1;
                    result = Math.max(result, dp[i]);
                }
            }
    
            // 改变元素
            for(int index=1; index<n; index++){
                int pre = index-dp[index];
                // 左附加一 dp[pre]+1
                if(pre>=0 && nums[pre]<100000){
                    result = Math.max(result, dp[pre]+1);
                }
                // 右附加一 dp[index]+1
                if(pre>=0 && nums[pre+1]>1){
                    result = Math.max(result, dp[index]+1);
                }
                // 合并情形一 dp[index]+dp[pre]
                if(pre>=0 && pre+2<n && nums[pre+2]-nums[pre]>=2){
                    result = Math.max(result, dp[index]+dp[pre]);
                }
                // 合并情形二 dp[index]+dp[pre]
                if(pre-1>=0 && nums[pre+1]-nums[pre-1]>=2){
                    result = Math.max(result, dp[index]+dp[pre]);
                }
            }
    
            return result;
        }
    }

  

