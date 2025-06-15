# java-NC397 统计子序列数


    import java.util.*;
    
    /**
     * NC397 统计子序列数
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串
         * @param t string字符串
         * @return int整型
         */
        public int countSubseq (String s, String t) {
            // return solution1(s, t);
            return solution2(s, t);
        }
    
        /**
         * 动态规划
         *
         * s[i:]表示s中从下标i到末尾的子字符串
         * t[j:]表示t中从下标j到末尾的子字符串
         * dp[i][j]表示在s[i:]子串中t[j:]子序列出现的次数
         *
         *            { dp[i+1][j+1] + dp[i+1][j]  , s.charAt(i) == t.charAt(j)
         * dp[i][j] = {
         *            { dp[i+1][j]                 , s.charAt(i) != t.charAt(j)
         *
         * 示例:
         *
         *     0 1 2 3 4 5 6 7 8 9
         * s:  n o w c o d e n o w
         *                   0 1 2
         * t:                n o w
         *
         * dp
         * i/j 0 1 2 3
         * 0   5 4 2 1
         * 1   1 4 2 1
         * 2   1 2 2 1
         * 3   1 2 1 1
         * 4   1 2 1 1
         * 5   1 1 1 1
         * 6   1 1 1 1
         * 7   1 1 1 1
         * 8   0 1 1 1
         * 9   0 0 1 1
         * 10  0 0 0 1
         *
         * @param s
         * @param t
         * @return
         */
        private int solution1(String s, String t){
            int m = s.length();
            int n = t.length();
    
            if(m < n){
                return 0;
            }
    
            int[][] dp = new int[m+1][n+1];
    
            // t[n:]为空串
            for(int i=0; i<=m; i++){
                dp[i][n] = 1;
            }
    
            // s[m:]为空串 t[j:]为非空串
            for(int j=0; j<n; j++){
                dp[m][j] = 0;
            }
    
            for(int i=m-1; i>=0; i--){
                for(int j=n-1; j>=0; j--){
                    if(s.charAt(i) == t.charAt(j)){
                        dp[i][j] = dp[i+1][j+1] + dp[i+1][j];
                    }else{
                        dp[i][j] = dp[i+1][j];
                    }
                }
            }
    
            return dp[0][0];
        }
    
        /**
         * 动态规划
         *
         * s[1:i]表示s中前i个字符组成的子字符串
         * t[1:j]表示t中前j个字符组成的子字符串
         * dp[i][j]表示在s[1:i]子串中t[1:j]子序列出现的次数
         *
         *            { dp[i-1][j-1] + dp[i-1][j]  , s.charAt(i-1) == t.charAt(j-1)
         * dp[i][j] = {
         *            { dp[i-1][j]                 , s.charAt(i-1) != t.charAt(j-1)
         *
         * 示例:
         *
         *     1 2 3 4 5 6 7 8 9 10
         * s:  n o w c o d e n o w
         *     1 2 3
         * t:  n o w
         *
         * dp
         * i/j 0 1 2 3
         * 0   1 0 0 0
         * 1   1 1 0 0
         * 2   1 1 1 0
         * 3   1 1 1 1
         * 4   1 1 1 1
         * 5   1 1 2 1
         * 6   1 1 2 1
         * 7   1 1 2 1
         * 8   1 2 2 1
         * 9   1 2 4 1
         * 10  1 2 4 5
         *
         * @param s
         * @param t
         * @return
         */
        private int solution2(String s, String t){
            int m = s.length();
            int n = t.length();
    
            if(m < n){
                return 0;
            }
    
            int[][] dp = new int[m+1][n+1];
    
            // t[:0]为空串
            for(int i=0; i<=m; i++){
                dp[i][0] = 1;
            }
    
            // s[:0]为空串 t[:j]为非空串
            for(int j=1; j<=n; j++){
                dp[0][j] = 0;
            }
    
            for(int i=1; i<=m; i++){
                for(int j=1; j<=n; j++){
                    if(s.charAt(i-1) == t.charAt(j-1)){
                        dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
                    }else{
                        dp[i][j] = dp[i-1][j];
                    }
                }
            }
    
            return dp[m][n];
        }
    }

  

