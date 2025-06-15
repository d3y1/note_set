# java-NC309 完全背包


    import java.util.*;
    
    /**
     * NC309 完全背包
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param v int整型
         * @param n int整型
         * @param nums int整型ArrayList<ArrayList<>>
         * @return int整型ArrayList
         */
        public ArrayList<Integer> knapsack (int v, int n, ArrayList<ArrayList<Integer>> nums) {
            // return solution1(v, n, nums);
            return solution2(v, n, nums);
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示背包体积为i时的最大价值
         *
         * 1. 背包能装物品的最大价值
         * dp[i] = Math.max(dp[i], dp[i-volume]+wealth)  , i>=volume
         *
         * 2. 背包能装物品的最大价值(背包恰好装满)
         *         { Math.max(dp[i], wealth)  , i=volume
         * dp[i] = {
         *         { Math.max(dp[i], dp[i-volume]+wealth)  , i>volume && dp[i-volume]>0
         *
         * @param v
         * @param n
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution1(int v, int n, ArrayList<ArrayList<Integer>> nums){
            ArrayList<Integer> result = new ArrayList<Integer>();
    
            int[] dp = new int[v+1];
            int volume,wealth;
    
            // 1. 背包能装物品的最大价值
            for(int i=1; i<=v; i++){
                for(int j=0; j<n; j++){
                    volume = nums.get(j).get(0);
                    wealth = nums.get(j).get(1);
                    if(i >= volume){
                        dp[i] = Math.max(dp[i], dp[i-volume]+wealth);
                    }
                }
            }
            result.add(dp[v]);
    
            // 2. 背包能装物品的最大价值(背包恰好装满)
            Arrays.fill(dp, 0);
            for(int i=1; i<=v; i++){
                for(int j=0; j<n; j++){
                    volume = nums.get(j).get(0);
                    wealth = nums.get(j).get(1);
                    if(i == volume){
                        dp[i] = Math.max(dp[i], wealth);
                    }
                    if(i > volume){
                        // i-volume能装满
                        if(dp[i-volume] > 0){
                            dp[i] = Math.max(dp[i], dp[i-volume]+wealth);
                        }
                    }
                }
            }
            result.add(dp[v]);
    
            return result;
        }
    
        /**
         * 动态规划
         * 
         * dp[i][0]表示背包体积为i时的最大价值
         * dp[i][1]表示背包体积为i时的最大价值(背包恰好装满)
         *
         * 1. 背包能装物品的最大价值
         * dp[i][0] = Math.max(dp[i][0], dp[i-volume][0]+wealth)  , i>=volume
         *
         * 2. 背包能装物品的最大价值(背包恰好装满)
         *            { Math.max(dp[i][1], wealth)  , i=volume
         * dp[i][1] = {
         *            { Math.max(dp[i][1], dp[i-volume][1]+wealth)  , i>volume && dp[i-volume][1]>0
         * 
         * @param v
         * @param n
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution2(int v, int n, ArrayList<ArrayList<Integer>> nums){
            ArrayList<Integer> result = new ArrayList<Integer>();
    
            int[][] dp = new int[v+1][2];
            int volume,wealth;
    
            // 1. 背包能装物品的最大价值 dp[i][0]
            // 2. 背包能装物品的最大价值(背包恰好装满) dp[i][1]
            for(int i=1; i<=v; i++){
                for(int j=0; j<n; j++){
                    volume = nums.get(j).get(0);
                    wealth = nums.get(j).get(1);
                    if(i == volume){
                        dp[i][0] = Math.max(dp[i][0], dp[i-volume][0]+wealth);
                        dp[i][1] = Math.max(dp[i][1], wealth);
                    }
                    if(i > volume){
                        dp[i][0] = Math.max(dp[i][0], dp[i-volume][0]+wealth);
                        // i-volume能装满
                        if(dp[i-volume][1] > 0){
                            dp[i][1] = Math.max(dp[i][1], dp[i-volume][1]+wealth);
                        }
                    }
                }
            }
            result.add(dp[v][0]);
            result.add(dp[v][1]);
    
            return result;
        }
    }

  

