# java-NC91 最长上升子序列(三)


    import java.util.*;
    
    /**
     * NC91 最长上升子序列(三)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * retrun the longest increasing subsequence
         * @param arr int整型一维数组 the array
         * @return int整型一维数组
         */
        public int[] LIS (int[] arr) {
            // return solution1(arr);
            return solution2(arr);
        }
    
        /**
         * 动态规划: 超时
         *
         * dp[i]表示从前面到以第i个数字结尾的最长上升子序列的长度(arr[i]必须被选取)
         *
         * dp[i] = Math.max(dp[i], dp[j]+1) , arr[j] < arr[i]
         *
         * @param arr
         * @return
         */
        private int[] solution1(int[] arr){
            int len = arr.length;
            if(len == 0){
                return new int[0];
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
    
            int[] result = new int[max];
            for(int i=len-1,j=max; j>0; i--){
                if(dp[i] == j){
                    result[--j] = arr[i];
                }
            }
    
            return result;
        }
    
        /**
         * 贪心 + 二分
         * @param arr
         * @return
         */
        private int[] solution2(int[] arr){
            int len = arr.length;
    
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
                    // 替换 或 附加
                    seq[pos+1] = arr[i];
                    dp[i] = pos + 1;
                }
            }
    
            int[] result = new int[max];
            for(int i=len-1,j=max; j>0; i--){
                if(dp[i] == j){
                    result[--j] = arr[i];
                }
            }
    
            return result;
        }
    }

  

