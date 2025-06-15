# java-NC196 编辑距离(一)


    import java.util.*;
    
    /**
     * NC196 编辑距离(一)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param str1 string字符串
         * @param str2 string字符串
         * @return int整型
         */
        public int editDistance (String str1, String str2) {
            return solution1(str1, str2);
            // return solution2(str1, str2);
        }
    
        /**
         * 动态规划: 二维数组
         *
         * dp[i][j]表示使字符串str1的前i个字符与字符串str2的前j个字符相同所需要的最少操作数
         *
         *            { dp[i-1][j-1]                                                    , str1.charAt(i-1) == str2.charAt(j-1)
         * dp[i][j] = {
         *            { Math.min(dp[i-1][j-1]+1, Math.min(dp[i-1][j]+1, dp[i][j-1]+1))  , str1.charAt(i-1) != str2.charAt(j-1)
         *
         * @param str1
         * @param str2
         * @return
         */
        private int solution1(String str1, String str2){
            int n1 = str1.length();
            int n2 = str2.length();
    
            int[][] dp = new int[n1+1][n2+1];
    
            // init 删除
            for(int i=0; i<=n1; i++){
                dp[i][0] = i;
            }
            // init 新增
            for(int j=0; j<=n2; j++){
                dp[0][j] = j;
            }
    
            for(int i=1; i<=n1; i++){
                for(int j=1; j<=n2; j++){
                    // 当前字符相同
                    if(str1.charAt(i-1) == str2.charAt(j-1)){
                        dp[i][j] = dp[i-1][j-1];
                    }
                    // 当前字符不同
                    else{
                        // str1 => str2
                        // 修改 dp[i-1][j-1]+1
                        // 删除 dp[i-1][j]+1
                        // 新增 dp[i][j-1]+1
                        dp[i][j] = Math.min(dp[i-1][j-1]+1, Math.min(dp[i-1][j]+1, dp[i][j-1]+1));
                    }
                }
            }
    
            return dp[n1][n2];
        }
    
        /**
         * 动态规划: 一维数组(空间压缩)
         *
         * dp[j]表示编辑成字符串str2的前j个字符所需要的最少操作数
         * 
         *         { pre                                            , str1.charAt(i-1) == str2.charAt(j-1)
         * dp[j] = {
         *         { Math.min(pre+1, Math.min(dp[j]+1, dp[j-1]+1))  , str1.charAt(i-1) != str2.charAt(j-1)
         *
         * @param str1
         * @param str2
         * @return
         */
        private int solution2(String str1, String str2){
            int n1 = str1.length();
            int n2 = str2.length();
    
            int[] dp = new int[n2+1];
            
            // init 新增
            for(int j=0; j<=n2; j++){
                dp[j] = j;
            }
    
            for(int i=1; i<=n1; i++){
                int pre = dp[0];
                // 重要
                dp[0] = i;
                for(int j=1; j<=n2; j++){
                    int tmp = dp[j];
    
                    // 当前字符相同
                    if(str1.charAt(i-1) == str2.charAt(j-1)){
                        dp[j] = pre;
                    }
                    // 当前字符不同
                    else{
                        // str1 => str2
                        // 修改 dp[i-1][j-1]+1 -> pre+1
                        // 删除 dp[i-1][j]+1   -> dp[j]+1
                        // 新增 dp[i][j-1]+1   -> dp[j-1]+1
                        dp[j] = Math.min(pre+1, Math.min(dp[j]+1, dp[j-1]+1));
                    }
                    pre = tmp;
                }
            }
    
            return dp[n2];
        }
    }

  
  

