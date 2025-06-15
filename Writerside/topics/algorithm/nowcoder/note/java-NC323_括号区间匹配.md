# java-NC323 括号区间匹配


    import java.util.*;
    
    /**
     * NC323 括号区间匹配
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串
         * @return int整型
         */
        public int match (String s) {
            return solution(s);
        }
    
        /**
         * 动态规划
         *
         * dp[i][j]表示使字符串s子串[i,j](从第i个字符到第j个字符)所有括号左右配对最少需要插入的括号数
         *
         * // case 1: ([[]) -> (s.charAt(i-1)=='('&&s.charAt(j-1)==')') || (s.charAt(i-1)=='['&&s.charAt(j-1)==']')
         * dp[i][j] = dp[i+1][j-1]                             , 1<=i<=n && i+1<=j<=n
         * // case 2: ([])()
         * dp[i][j] = Math.min(dp[i][j], dp[i][k]+dp[k+1][j])  , 1<=i<=n && i+1<=j<=n && i<=k<j
         *
         * @param s
         * @return
         */
        private int solution(String s){
            int n = s.length();
    
            int[][] dp = new int[n+1][n+1];
            for(int i=n; i>0; i--){
                dp[i][i] = 1;
                for(int j=i+1; j<=n; j++){
                    dp[i][j] = Integer.MAX_VALUE;
                    // case 1: ([[])
                    if((s.charAt(i-1)=='('&&s.charAt(j-1)==')') || (s.charAt(i-1)=='['&&s.charAt(j-1)==']')){
                        dp[i][j] = dp[i+1][j-1];
                    }
                    // case 2: ([])()
                    for(int k=i; k<j; k++){
                        dp[i][j] = Math.min(dp[i][j], dp[i][k]+dp[k+1][j]);
                    }
                }
            }
    
            return dp[1][n];
        }
    }

  

