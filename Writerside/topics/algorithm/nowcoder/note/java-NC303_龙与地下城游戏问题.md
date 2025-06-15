# java-NC303 龙与地下城游戏问题


    import java.util.*;
    
    /**
     * NC303 龙与地下城游戏问题
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param mp int整型ArrayList<ArrayList<>>
         * @return int整型
         */
        public int dnd (ArrayList<ArrayList<Integer>> mp) {
            return solution(mp);
        }
    
        /**
         * 动态规划: 注意从右下角往左上角逆序遍历!
         *
         * dp[i][j]表示在位置(i,j)处(第i行第j列)所需要的最少血量
         * 
         *            { Math.max(1-mp.get(i-1).get(j-1), 1)                                 , i==n && j==m
         * dp[i][j] = { Math.max(dp[i][j+1]-mp.get(i-1).get(j-1), 1)                        , i==n && j<m
         *            { Math.max(dp[i+1][j]-mp.get(i-1).get(j-1), 1)                        , i<n && j==m
         *            { Math.max(Math.min(dp[i][j+1], dp[i+1][j])-mp.get(i-1).get(j-1), 1)  , i<n && j<m
         *
         * @param mp
         * @return
         */
        private int solution(ArrayList<ArrayList<Integer>> mp){
            int n = mp.size();
            int m = mp.get(0).size();
    
            int[][] dp = new int[n+1][m+1];
    
            for(int i=n; i>0; i--){
                for(int j=m; j>0; j--){
                    // 在右下角 最终位置
                    // 到达位置(i,j)处 遭遇怪兽或血瓶前: 血量至少为1 => 所需最少血量: 1
                    // 到达位置(i,j)处 遭遇怪兽或血瓶后: 血量至少为1 => 所需最少血量: 1-mp.get(i-1).get(j-1)
                    // 需要同时保证上面2点
                    if(i==n && j==m){
                        dp[i][j] = Math.max(1-mp.get(i-1).get(j-1), 1);
                    }
                    // 最下一行 只能向右
                    // 到达位置(i,j)处 遭遇怪兽或血瓶前: 血量至少为1 => 所需最少血量: 1
                    // 到达位置(i,j)处 遭遇怪兽或血瓶后: 血量至少为dp[i][j+1] => 所需最少血量: dp[i][j+1]-mp.get(i-1).get(j-1)
                    // 需要同时保证上面2点
                    else if(i==n && j<m){
                        dp[i][j] = Math.max(dp[i][j+1]-mp.get(i-1).get(j-1), 1);
                    }
                    // 最右一列 只能向下
                    // 到达位置(i,j)处 遭遇怪兽或血瓶前: 血量至少为1 => 所需最少血量: 1
                    // 到达位置(i,j)处 遭遇怪兽或血瓶后: 血量至少为dp[i+1][j] => 所需最少血量: dp[i+1][j]-mp.get(i-1).get(j-1)
                    // 需要同时保证上面2点
                    else if(i<n && j==m){
                        dp[i][j] = Math.max(dp[i+1][j]-mp.get(i-1).get(j-1), 1);
                    }
                    // 可以向右 可以向下
                    // 到达位置(i,j)处 遭遇怪兽或血瓶前: 血量至少为1 => 所需最少血量: 1
                    // 到达位置(i,j)处 遭遇怪兽或血瓶后: 血量至少为min(dp[i][j+1], dp[i+1][j]) => 所需最少血量: min(dp[i][j+1], dp[i+1][j])-mp.get(i-1).get(j-1)
                    // 需要同时保证上面2点
                    else{
                        dp[i][j] = Math.max(Math.min(dp[i][j+1], dp[i+1][j])-mp.get(i-1).get(j-1), 1);
                    }
                }
            }
    
            return dp[1][1];
        }
    }

  

