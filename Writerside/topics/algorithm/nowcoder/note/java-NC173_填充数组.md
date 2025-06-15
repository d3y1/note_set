# java-NC173 填充数组


    import java.util.*;
    
    /**
     * NC173 填充数组
     * @author d3y1
     */
    public class Solution {
        private final int MOD = 1000000007;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param a int整型一维数组
         * @param k int整型
         * @return int整型
         */
        public int FillArray (int[] a, int k) {
            // return solution1(a, k);
            return solution2(a, k);
        }
    
        /**
         * 动态规划
         *
         * left  取值左边界 2
         * right 取值右边界 5
         * 区间取值个数j = right - left + 1 = 5 - 2 + 1 = 4 (2,3,4,5)
         * dp[j]表示以区间中某值为开始的填充方案数(其实与具体的取值无关, 仅与取值区间大小有关)
         *
         * 举例子找规律:
         * 2 0 5
         *   2
         *   3
         *   4
         *   5
         *
         * 填充0个数i: 1 (0)
         * 取值个数j: 4 (2,3,4,5)
         * dp[2] = 1
         * dp[3] = 1
         * dp[4] = 1
         * dp[5] = 1
         * 等价于
         * dp[1] = 1
         * dp[2] = 1
         * dp[3] = 1
         * dp[4] = 1
         *
         * 2 0 0 5
         *   2 2
         *   2 3
         *   2 4
         *   2 5
         *
         *   3 3
         *   3 4
         *   3 5
         *
         *   4 4
         *   4 5
         *
         *   5 5
         *
         * 填充0个数i: 2 (0 0)
         * 取值个数j: 4 (2,3,4,5)
         * dp[2] = 4
         * dp[3] = 3
         * dp[4] = 2
         * dp[5] = 1
         * 等价于
         * dp[1] = 4
         * dp[2] = 3
         * dp[3] = 2
         * dp[4] = 1
         *
         * 2 0 0 0 5
         *   2 2 2
         *   2 2 3
         *   2 2 4
         *   2 2 5
         *   2 3 3
         *   2 3 4
         *   2 3 5
         *   2 4 4
         *   2 4 5
         *   2 5 5
         *
         *   3 3 3
         *   3 3 4
         *   3 3 5
         *   3 4 4
         *   3 4 5
         *   3 5 5
         *
         *   4 4 4
         *   4 4 5
         *   4 5 5
         *
         *   5 5 5
         *
         * 填充0个数i: 3 (0 0 0)
         * 取值个数j: 4 (2,3,4,5)
         * dp[2] = 10
         * dp[3] = 6
         * dp[4] = 3
         * dp[5] = 1
         * 等价于
         * dp[1] = 10
         * dp[2] = 6
         * dp[3] = 3
         * dp[4] = 1
         *
         * 可见
         * i / j 1  2  3  4
         * 1     1  1  1  1
         * 2     4  3  2  1
         * 3     10 6  3  1
         *
         * @param a
         * @param k
         * @return
         */
        private int solution1(int[] a, int k){
            long[] dp = new long[1001];
    
            int n = a.length;
            int[] A = new int[n+2];
            for(int i=1; i<=n; i++){
                A[i] = a[i-1];
            }
            // 补充左右边界 便于后续处理
            A[0] = 1;
            A[n+1] = k;
    
            int left = A[0];
            int right = 0;
            int gap = 0;
            long sum = 0;
            long result = 0;
            for(int i=1; i<n+2; i++){
                if(A[i] > 0){
                    if(gap == 0){
                        left = A[i];
                    }else if(gap > 0){
                        right = A[i];
                        Arrays.fill(dp, 1);
                        for(int times=1; times<=gap; times++){
                            sum = 0;
                            for(int j=right-left+1; j>=1; j--){
                                sum = (sum + dp[j]) % MOD;
                                dp[j] = sum;
                            }
                        }
                        if(result == 0){
                            result = sum % MOD;
                        }else if(result > 0){
                            result = (result * sum) % MOD;
                        }
                        left = right;
                        gap = 0;
                    }
                }else if(A[i] == 0){
                    gap++;
                }
            }
    
            return (int)result;
        }
    
        /**
         * 动态规划
         *
         * left  取值左边界 2
         * right 取值右边界 5
         * 区间取值个数j = right - left + 1 = 5 - 2 + 1 = 4 (2,3,4,5)
         * dp[j]表示以区间中某值为开始的填充方案数(其实与具体的取值无关, 仅与取值区间大小有关)
         *
         * 举例子找规律:
         * 2 0 5
         *   2
         *   3
         *   4
         *   5
         *
         * 填充0个数i: 1 (0)
         * 取值个数j: 4 (2,3,4,5)
         * dp[2] = 1
         * dp[3] = 1
         * dp[4] = 1
         * dp[5] = 1
         * 等价于
         * dp[1] = 1
         * dp[2] = 1
         * dp[3] = 1
         * dp[4] = 1
         *
         * 2 0 0 5
         *   2 2
         *   2 3
         *   2 4
         *   2 5
         *
         *   3 3
         *   3 4
         *   3 5
         *
         *   4 4
         *   4 5
         *
         *   5 5
         *
         * 填充0个数i: 2 (0 0)
         * 取值个数j: 4 (2,3,4,5)
         * dp[2] = 4
         * dp[3] = 3
         * dp[4] = 2
         * dp[5] = 1
         * 等价于
         * dp[1] = 1
         * dp[2] = 2
         * dp[3] = 3
         * dp[4] = 4
         *
         * 2 0 0 0 5
         *   2 2 2
         *   2 2 3
         *   2 2 4
         *   2 2 5
         *   2 3 3
         *   2 3 4
         *   2 3 5
         *   2 4 4
         *   2 4 5
         *   2 5 5
         *
         *   3 3 3
         *   3 3 4
         *   3 3 5
         *   3 4 4
         *   3 4 5
         *   3 5 5
         *
         *   4 4 4
         *   4 4 5
         *   4 5 5
         *
         *   5 5 5
         *
         * 填充0个数i: 3 (0 0 0)
         * 取值个数j: 4 (2,3,4,5)
         * dp[2] = 10
         * dp[3] = 6
         * dp[4] = 3
         * dp[5] = 1
         * 等价于
         * dp[1] = 1
         * dp[2] = 3
         * dp[3] = 6
         * dp[4] = 10
         *
         * 可见
         * i / j 1  2  3  4
         * 1     1  1  1  1
         * 2     1  2  3  4
         * 3     1  3  6  10
         *
         * 由上可知
         * dp[i][j]表示填充个数为i且取值个数为j时的填充方案数
         * dp[i][j] = dp[i-1][j] + dp[i][j-1]
         *
         * @param a
         * @param k
         * @return
         */
        private int solution2(int[] a, int k){
            int n = a.length;
    
            int[][] dp = new int[n+1][k+1];
    
            for(int j=1; j<=k; j++){
                dp[1][j] = j;
            }
            for(int i=1; i<=n; i++){
                for(int j=1; j<=k; j++){
                    if(i == 1){
                        dp[i][j] = j;
                    }else{
                        dp[i][j] = (dp[i-1][j] + dp[i][j-1]) % MOD;
                    }
                }
            }
            
            int[] A = new int[n+2];
            for(int i=1; i<=n; i++){
                A[i] = a[i-1];
            }
            // 补充左右边界 便于后续处理
            A[0] = 1;
            A[n+1] = k;
    
            int left = A[0];
            int right = 0;
            int gap = 0;
            long sum = 0;
            long result = 1;
            for(int i=1; i<n+2; i++){
                if(A[i] > 0){
                    if(gap == 0){
                        left = A[i];
                    }else if(gap > 0){
                        right = A[i];
                        sum = dp[gap][right-left+1];
                        result = (result * sum) % MOD;
                        left = right;
                        gap = 0;
                    }
                }else if(A[i] == 0){
                    gap++;
                }
            }
            
            return (int)result;
        }
    }

  

