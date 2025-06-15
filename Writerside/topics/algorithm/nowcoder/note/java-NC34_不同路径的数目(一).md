# java-NC34 不同路径的数目(一)


    import java.util.*;
    
    /**
     * NC34 不同路径的数目(一)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param m int整型
         * @param n int整型
         * @return int整型
         */
        public int uniquePaths (int m, int n) {
            return solution1(m, n);
            // return solution2(m, n);
            // return solution3(m, n);
            // return solution4(m, n);
        }
    
        /**
         * 动态规划: 二维数组
         *
         * dp[i][j]表示从地图左上角(1,1)到达当前位置(i,j)的路径数
         *
         * dp[i][j] = dp[i-1][j] + dp[i][j-1]
         *
         * @param m
         * @param n
         * @return
         */
        private int solution1(int m, int n){
            if(m==1 || n==1){
                return 1;
            }
    
            int[][] dp = new int[m+1][n+1];
            for(int i=1; i<=m; i++){
                dp[i][1] = 1;
            }
            for(int i=1; i<=n; i++){
                dp[1][i] = 1;
            }
    
            for(int i=2; i<=m; i++){
                for(int j=2; j<=n; j++){
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
            }
    
            return dp[m][n];
        }
    
        /**
         * 动态规划: 一维数组(空间压缩)
         * 
         * dp[j]表示从地图左上角(第1列)到达当前位置(第j列)的路径数
         * 
         * dp[j] = dp[j] + dp[j-1]
         * 
         * @param m
         * @param n
         * @return
         */
        private int solution2(int m, int n){
            if(m==1 || n==1){
                return 1;
            }
    
            int[] dp = new int[n+1];
            for(int i=1; i<=n; i++){
                dp[i] = 1;
            }
    
            for(int i=2; i<=m; i++){
                for(int j=2; j<=n; j++){
                    dp[j] = dp[j] + dp[j-1];
                }
            }
    
            return dp[n];
        }
    
        /**
         * 递归
         * @param m
         * @param n
         * @return
         */
        private int solution3(int m, int n){
            if(m==1 || n==1){
                return 1;
            }
            
            return solution3(m-1, n)+solution3(m, n-1);
        }
    
        /**
         * 组合数学
         *
         * 从矩阵左上角走到矩阵右下角, 总共需要走m+n−2步:
         * 往下走m−1步
         * 往右走n−1步
         * 不同的走法路径对应于往下和往右的组合情况
         *
         * 等价于:
         * 从m+n−2步中选取m-1步往下走的组合个数: C(m+n-2, m-1) = (m+n-2)! / ((n-1)!(m-1)!) = (n*(n+1)*...*(m+n-2)) / (m-1)!
         *
         * @param m
         * @param n
         * @return
         */
        private int solution4(int m, int n){
            long result = 1;
            for(int i=1,j=n; i<=m-1; i++,j++){
                result = result * j/i;
            }
    
            return (int)result;
        }
    }

  

