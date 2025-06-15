# java-NC127 最长公共子串


    import java.util.*;
    
    /**
     * NC127 最长公共子串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * longest common substring
         * @param str1 string字符串 the string
         * @param str2 string字符串 the string
         * @return string字符串
         */
        public String LCS (String str1, String str2) {
            return solution(str1, str2);
        }
    
        /**
         * 动态规划
         * 
         * dp[i][j]表示str1中以第i个字符结尾且str2中以第j个字符结尾的公共子串的长度
         * 
         *            { 0                 , str1.charAt(i-1) != str2.charAt(j-1)
         * dp[i][j] = {
         *            { dp[i-1][j-1] + 1  , str1.charAt(i-1) == str2.charAt(j-1)
         * 
         * @param str1
         * @param str2
         * @return
         */
        private String solution(String str1, String str2){
            int len1 = str1.length();
            int len2 = str2.length();
    
            int[][] dp = new int[len1+1][len2+1];
            int len = 0;
            int index = 0;
            for(int i=1; i<=len1; i++){
                for(int j=1; j<=len2; j++){
                    if(str1.charAt(i-1) == str2.charAt(j-1)){
                        dp[i][j] = dp[i-1][j-1] + 1;
                        if(dp[i][j] > len){
                            len = dp[i][j];
                            index = i;
                        }
                    }
                }
            }
    
            return str1.substring(index-len, index);
        }
    }

  

