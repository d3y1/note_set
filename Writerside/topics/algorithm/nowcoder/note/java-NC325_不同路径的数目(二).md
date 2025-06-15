# java-NC325 不同路径的数目(二)


    import java.util.*;
    
    /**
     * NC325 不同路径的数目(二)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param obstacleGrid char字符型ArrayList<ArrayList<>>
         * @return int整型
         */
        public int uniquePathsWithObstacles (ArrayList<ArrayList<Character>> obstacleGrid) {
            return solution(obstacleGrid);
        }
    
        /**
         * 动态规划
         *
         * dp[i][j]表示机器人移动到地图第i行第j列处的不同路径数
         * 
         *            { 1                        , i=1 && j=1
         * dp[i][j] = { dp[i][j-1]               , i=1 && j>1
         *            { dp[i-1][j]               , i>1 && j=1
         *            { dp[i][j-1] + dp[i-1][j]  , i>1 && j>1
         *
         * @param obstacleGrid
         * @return
         */
        private int solution(ArrayList<ArrayList<Character>> obstacleGrid){
            int m = obstacleGrid.size();
            int n = obstacleGrid.get(0).size();
    
            int[][] dp = new int[m+1][n+1];
    
            for(int i=1; i<=m; i++){
                for(int j=1; j<=n; j++){
                    if(i==1 && j==1){
                        if(obstacleGrid.get(i-1).get(j-1) != '#'){
                            dp[i][j] = 1;
                        }
                    }else if(i==1 && j>1){
                        if(obstacleGrid.get(i-1).get(j-1) != '#'){
                            dp[i][j] = dp[i][j-1];
                        }
                    }else if(i>1 && j==1){
                        if(obstacleGrid.get(i-1).get(j-1) != '#'){
                            dp[i][j] = dp[i-1][j];
                        }
                    }else{
                        if(obstacleGrid.get(i-1).get(j-1) != '#'){
                            dp[i][j] = dp[i][j-1] + dp[i-1][j];
                        }
                    }
                }
            }
    
            return dp[m][n];
        }
    }

  

