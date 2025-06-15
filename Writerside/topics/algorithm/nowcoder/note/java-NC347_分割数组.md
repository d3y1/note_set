# java-NC347 分割数组


    import java.util.*;
    
    /**
     * NC347 分割数组
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param num int整型ArrayList
         * @param m int整型
         * @return int整型
         */
        public int splitMin (ArrayList<Integer> num, int m) {
            return solution1(num, m);
            // return solution2(num, m);
        }
    
        /**
         * 动态规划
         *
         * dp[i][j]表示数组num前i个数分成j个非空连续子数组的最小的最大和(非空连续子数组)
         *
         * dp[i][j] = Math.min(dp[i][j], Math.max(dp[k][j-1], sum))  , 1<=i<=n && 1<=j<=min(i,m) && j-1<=k<=i-1
         *
         * @param num
         * @param m
         * @return
         */
        private int solution1(ArrayList<Integer> num, int m){
            int n = num.size();
    
            int[][] dp = new int[n+1][m+1];
    
            // 前i个数
            for(int i=1; i<=n; i++){
                // 分成j个非空连续子数组
                for(int j=1; j<=i&&j<=m; j++){
                    dp[i][j] = Integer.MAX_VALUE;
                    int sum = 0;
                    // 前k个数分成j-1个非空连续子数组
                    for(int k=i-1; k>=j-1; k--){
                        // sum = num[k+1,i] -> 第k+1到第i个数的和
                        sum += num.get(k);
                        // dp[k][j-1]: 数组num前k个数分成0个非空连续子数组 -> 无法实现
                        if(k>0 && j-1==0){
                            continue;
                        }
                        dp[i][j] = Math.min(dp[i][j], Math.max(dp[k][j-1], sum));
                    }
                }
            }
    
            return dp[n][m];
        }
    
        /**
         * 二分 + 贪心
         * @param num
         * @param m
         * @return
         */
        private int solution2(ArrayList<Integer> num, int m){
            int n = num.size();
            int max=0, sum=0;
            int val;
            for(int i=0; i<n; i++){
                val = num.get(i);
                max = Math.max(max, val);
                sum += val;
            }
    
            int left = max;
            int right = sum;
            int mid;
            // 二分
            while(left <= right){
                mid = (left+right)/2;
                int cnt=1;
                int part = 0;
                for(int curr: num){
                    // 贪心
                    if(part+curr > mid){
                        cnt++;
                        part = curr;
                    }else{
                        part += curr;
                    }
                }
                if(cnt > m){
                    left = mid+1;
                }else{
                    right = mid-1;
                }
            }
    
            return left;
        }
    }

  

