# java-NC225 三角形最小路径和


    import java.util.*;
    
    /**
     * NC225 三角形最小路径和
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param triangle int整型二维数组
         * @return int整型
         */
        public int minTrace (int[][] triangle) {
            return solution1(triangle);
            // return solution2(triangle);
        }
    
        /**
         * 动态规划: 二维数组
         *
         * dp[i][j]表示到达第i行第j列时的最小路径和
         * 
         *            { dp[i-1][j]+triangle[i-1][j-1]                                             , j=1
         * dp[i][j] = { dp[i-1][j-1]+triangle[i-1][j-1]                                           , j=i
         *            { Math.min(dp[i-1][j-1]+triangle[i-1][j-1], dp[i-1][j]+triangle[i-1][j-1])  , 1<j<i
         *
         * @param triangle
         * @return
         */
        private int solution1(int[][] triangle){
            int row = triangle.length;
            if(row == 1){
                return triangle[0][0];
            }
    
            int[][] dp = new int[row+1][row+1];
            dp[1][1] = triangle[0][0];
    
            int result = Integer.MAX_VALUE;
            for(int i=2; i<=row; i++){
                for(int j=1; j<=i; j++){
                    if(j == 1){
                        dp[i][j] = dp[i-1][j]+triangle[i-1][j-1];
                        continue;
                    }
                    if(j == i){
                        dp[i][j] = dp[i-1][j-1]+triangle[i-1][j-1];
                        continue;
                    }
                    dp[i][j] = Math.min(dp[i-1][j-1]+triangle[i-1][j-1], dp[i-1][j]+triangle[i-1][j-1]);
                    if(i == row){
                        result = Math.min(result, dp[i][j]);
                    }
                }
            }
    
            return result;
        }
    
        /**
         * 动态规划: 一维数组(空间压缩)
         * 
         * dp[j]表示到达第j列时的最小路径和
         * 
         *         { dp[j]+triangle[i-1][j-1]                                    , j=1
         * dp[j] = { pre+triangle[i-1][j-1]                                      , j=i
         *         { Math.min(dp[j]+triangle[i-1][j-1], pre+triangle[i-1][j-1])  , 1<j<i
         * 
         * @param triangle
         * @return
         */
        private int solution2(int[][] triangle){
            int row = triangle.length;
            if(row == 1){
                return triangle[0][0];
            }
    
            int[] dp = new int[row+1];
            dp[1] = triangle[0][0];
    
            int result = Integer.MAX_VALUE;
            for(int i=2; i<=row; i++){
                int pre = dp[1];
                for(int j=1; j<=i; j++){
                    int tmp = dp[j];
                    if(j == 1){
                        dp[j] = dp[j]+triangle[i-1][j-1];
                        continue;
                    }
                    if(j == i){
                        dp[j] = pre+triangle[i-1][j-1];
                        continue;
                    }
                    dp[j] = Math.min(dp[j]+triangle[i-1][j-1], pre+triangle[i-1][j-1]);
                    if(i == row){
                        result = Math.min(result, dp[j]);
                    }
                    pre = tmp;
                }
            }
    
            return result;
        }
    }

  

