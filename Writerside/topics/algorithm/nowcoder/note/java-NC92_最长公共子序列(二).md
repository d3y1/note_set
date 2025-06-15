# java-NC92 最长公共子序列(二)


    import java.util.*;
    
    /**
     * NC92 最长公共子序列(二)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * longest common subsequence
         * @param s1 string字符串 the string
         * @param s2 string字符串 the string
         * @return string字符串
         */
        public String LCS (String s1, String s2) {
            return solution(s1, s2);
        }
    
        /**
         * 动态规划
         *
         * dp[i][j]表示在s1中以第i个字符结尾, s2中以第j个字符结尾时的最长公共子序列长度
         * 
         *            { dp[i-1][j-1]+1                   , s1.charAt(i-1)==s2.charAt(j-1)
         * dp[i][j] = { 
         *            { Math.max(dp[i-1][j], dp[i][j-1]) , s1.charAt(i-1)!=s2.charAt(j-1)
         *            
         * @param s1
         * @param s2
         * @return
         */
        private String solution(String s1, String s2){
            int len1 = s1.length();
            int len2 = s2.length();
    
            if(len1==0 || len2==0){
                return "-1";
            }
    
            int[][] dp = new int[len1+1][len2+1];
            for(int i=1; i<=len1; i++){
                for(int j=1; j<=len2; j++){
                    dp[i][j] = (s1.charAt(i-1)==s2.charAt(j-1)) ? dp[i-1][j-1]+1 : Math.max(dp[i-1][j], dp[i][j-1]);
                }
            }
    
            StringBuilder sb = new StringBuilder();
            for(int i=len1,j=len2; dp[i][j]>=1; ){
                if(s1.charAt(i-1) == s2.charAt(j-1)){
                    sb.append(s1.charAt(i-1));
                    i--;
                    j--;
                }else if(dp[i-1][j] >= dp[i][j-1]){
                    i--;
                }else{
                    j--;
                }
            }
    
            return sb.toString().isEmpty() ? "-1" : sb.reverse().toString();
        }
    }

  

