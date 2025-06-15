# java-NC376 变回文串的最少插入次数


    import java.util.*;
    
    /**
     * NC376 变回文串的最少插入次数
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param str string字符串
         * @return int整型
         */
        public int minInsert (String str) {
            return solution1(str);
            // return solution2(str);
            // return solution3(str);
            // return solution33(str);
        }
    
        /**
         * 动态规划+双指针+贪心
         *
         * dp[i][j]表示字符串str子串[i,j]变成回文串的最少插入次数
         *
         *            { Math.min(dp[i+1][j]+1, dp[i][j-1]+1)               , str.charAt(i) != str.charAt(j)
         * dp[i][j] = {
         *            { Math.min(dp[i+1][j]+1, dp[i][j-1]+1, dp[i+1][j-1]) , str.charAt(i) == str.charAt(j)
         *
         * @param str
         * @return
         */
        private int solution1(String str){
            int n = str.length();
            int[][] dp = new int[n][n];
    
            // 双指针
            for(int i=n-2; i>=0; i--){
                for(int j=i+1; j<n; j++){
                    // 贪心
                    dp[i][j] = Math.min(dp[i+1][j]+1, dp[i][j-1]+1);
                    if(str.charAt(i) == str.charAt(j)){
                        dp[i][j] = Math.min(dp[i][j], dp[i+1][j-1]);
                    }
                }
            }
    
            return dp[0][n-1];
        }
    
        // /**
        //  * 动态规划
        //  *
        //  * dp[i][j]表示字符串str子串[i,j]变成回文串的最少插入次数
        //  *
        //  *            { dp[i+1][j-1]                        , str.charAt(i)=str.charAt(j)
        //  * dp[i][j] = {
        //  *            { Math.min(dp[i+1][j], dp[i][j-1])+1  , str.charAt(i)!=str.charAt(j)
        //  *
        //  * @param str
        //  * @return
        //  */
        // private int solution2(String str){
        //     int n = str.length();
        //     int[][] dp = new int[n][n];
    
        //     for(int i=n-2; i>=0; i--){
        //         for(int j=i+1; j<n; j++){
        //             if(str.charAt(i) == str.charAt(j)){
        //                 dp[i][j] = dp[i+1][j-1];
        //             }else{
        //                 dp[i][j] = Math.min(dp[i+1][j], dp[i][j-1])+1;
        //             }
        //         }
        //     }
    
        //     return dp[0][n-1];
        // }
    
        // /**
        //  * 动态规划
        //  *
        //  * 转化为 -> LCS(Longest Common Subsequence) 最长公共子序列 问题
        //  *
        //  * dp[i][j]表示s1以第i个字符结尾且s2以第j个字符结尾的最长公共子序列的长度
        //  *
        //  *            { dp[i-1][j-1] + 1                             , s1.charAt(i-1) == s2.charAt(j-1)
        //  * dp[i][j] = {
        //  *            { dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1])  , s1.charAt(i-1) != s2.charAt(j-1)
        //  *
        //  * result = n-LCS(str, str.reverse())
        //  *
        //  * @param str
        //  * @return
        //  */
        // private int solution3(String str){
        //     String s1 = str;
        //     String s2 = new StringBuilder(str).reverse().toString();
        //     int n1 = s1.length();
        //     int n2 = s2.length();
    
        //     int[][] dp = new int[n1+1][n2+1];
    
        //     for(int i=1; i<=n1; i++){
        //         for(int j=1; j<=n2; j++){
        //             if(s1.charAt(i-1) == s2.charAt(j-1)){
        //                 dp[i][j] = dp[i-1][j-1] + 1;
        //             }else{
        //                 dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
        //             }
        //         }
        //     }
    
        //     return n1-dp[n1][n2];
        // }
    
        /**
         * 动态规划+双指针+贪心
         *
         * 转化为 -> LCS(Longest Common Subsequence) 最长公共子序列 问题
         *
         * dp[i][j]表示s1以第i个字符结尾且s2以第j个字符结尾的最长公共子序列的长度
         *
         *            { Math.max(dp[i-1][j], dp[i][j-1])                  , s1.charAt(i-1) != s2.charAt(j-1)
         * dp[i][j] = {
         *            { Math.max(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]+1)  , s1.charAt(i-1) == s2.charAt(j-1)
         *
         * result = n-LCS(str, str.reverse())
         *
         * @param str
         * @return
         */
        private int solution33(String str){
            String s1 = str;
            String s2 = new StringBuilder(str).reverse().toString();
            int n1 = s1.length();
            int n2 = s2.length();
    
            int[][] dp = new int[n1+1][n2+1];
    
            // 双指针
            for(int i=1; i<=n1; i++){
                for(int j=1; j<=n2; j++){
                    // 贪心
                    dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
                    if(s1.charAt(i-1) == s2.charAt(j-1)){
                        dp[i][j] = Math.max(dp[i][j], dp[i-1][j-1]+1);
                    }
                }
            }
    
            return n1-dp[n1][n2];
        }
    }

  

