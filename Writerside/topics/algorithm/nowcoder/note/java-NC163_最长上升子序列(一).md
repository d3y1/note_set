# java-NC163 最长上升子序列(一)


    import java.util.*;
    
    /**
     * NC163 最长上升子序列(一)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 给定数组的最长严格上升子序列的长度。
         * @param arr int整型一维数组 给定的数组
         * @return int整型
         */
        public int LIS (int[] arr) {
            return solution1(arr);
            // return solution2(arr);
            // return solution3(arr);
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示从前面到以第i个数字结尾的最长上升子序列的长度(arr[i]必须被选取)
         *
         * dp[j] = Math.max(dp[j], dp[i]+1)  , (arr[i] < arr[j])
         *
         * @param arr
         * @return
         */
        private int solution1(int[] arr){
            int len = arr.length;
    
            if(len <= 1){
                return len;
            }
    
            int[] dp = new int[len];
    
            Arrays.fill(dp, Integer.valueOf(1));
    
            int result = 1;
            for(int i=0; i<len; i++){
                for(int j=i+1; j<len; j++){
                    if(arr[i] < arr[j]){
                        dp[j] = Math.max(dp[j], dp[i]+1);
                        result = Math.max(result, dp[j]);
                    }
                }
            }
    
            return result;
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示从前面到以第i个数字结尾的最长上升子序列的长度(arr[i]必须被选取)
         *
         * dp[i] = Math.max(dp[i], dp[j]+1) , arr[j] < arr[i]
         *
         * @param arr
         * @return
         */
        private int solution2(int[] arr){
            int len = arr.length;
    
            if(len <= 1){
                return len;
            }
    
            int[] dp = new int[len];
    
            // 初始值
            dp[0] = 1;
            // 最长上升子序列的长度
            int max = 1;
            for(int i=1; i<len; i++){
                dp[i] = 1;
                for(int j=0; j<i; j++){
                    if(arr[j] < arr[i]){
                        dp[i] = Math.max(dp[i], dp[j]+1);
                    }
                }
                max = Math.max(max, dp[i]);
            }
            
            return max;
        }
    
        /**
         * 贪心 + 二分
         * @param arr
         * @return
         */
        private int solution3(int[] arr){
            int len = arr.length;
    
            if(len <= 1){
                return len;
            }
    
            // 表示从前面到以第i个数字结尾的最长上升子序列的长度(arr[i]必须被选取)
            int[] dp = new int[len];
            // 最长上升子序列 单调增
            int[] seq = new int[len+1];
            seq[1] = arr[0];
            dp[0] = 1;
            // 最长上升子序列的长度
            int max = 1;
    
            for(int i=1; i<len; i++){
                if(seq[max] < arr[i]){
                    seq[++max] = arr[i];
                    dp[i] = max;
                }else{
                    int left=1,right=max;
                    // 上升子序列seq中二分查找最大的小于arr[i]的位置pos
                    int pos = 0;
                    while(left <= right){
                        int mid = (left + right) >> 1;
                        if(seq[mid] < arr[i]){
                            pos = mid;
                            left = mid + 1;
                        }else{
                            right = mid - 1;
                        }
                    }
                    // 替换
                    seq[pos+1] = arr[i];
                    dp[i] = pos + 1;
                }
            }
    
            return max;
        }
    }

  

