# java-NC228 判断子序列


    import java.util.*;
    
    /**
     * NC228 判断子序列
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param S string字符串
         * @param T string字符串
         * @return bool布尔型
         */
        public boolean isSubsequence (String S, String T) {
            // return solution1(S,T);
            return solution11(S,T);
            // return solution2(S,T);
            // return solution22(S,T);
            // return solution3(S,T);
            // return solution33(S,T);
            // return solution4(S,T);
            // return solution44(S,T);
        }
    
        /**
         * 双指针
         * @param S
         * @param T
         * @return
         */
        private boolean solution1(String S, String T){
            int lenS = S.length();
            int lenT = T.length();
            if(lenS > lenT){
                return false;
            }
    
            // 双指针
            int i = 0;
            int j = 0;
            while(i<lenS && j<lenT){
                if(S.charAt(i) == T.charAt(j)){
                    i++;
                    j++;
                }else{
                    j++;
                }
            }
    
            return i==lenS;
        }
    
        /**
         * 双指针
         * @param S
         * @param T
         * @return
         */
        private boolean solution11(String S, String T){
            int lenS = S.length();
            int lenT = T.length();
            if(lenS > lenT){
                return false;
            }
    
            // 双指针
            for(int i=0,j=0; i<lenS&&j<lenT; j++){
                if(S.charAt(i) == T.charAt(j)){
                    i++;
                }
                if(i == lenS){
                    return true;
                }
            }
    
            return false;
        }
    
        /**
         * 动态规划: 二维数组
         *
         * 转化为: 最长公共子序列问题
         *
         * dp[i][j]表示S以第i个字符结尾(S[0,i-1])且T以第j个字符结尾(T[0,j-1])的最长公共子序列的长度
         *
         *            { dp[i-1][j-1] + 1                  , S.charAt(i-1) == T.charAt(j-1)
         * dp[i][j] = {
         *            { Math.max(dp[i-1][j], dp[i][j-1])  , S.charAt(i-1) != T.charAt(j-1)
         *
         * @param S
         * @param T
         * @return
         */
        private boolean solution2(String S, String T){
            int lenS = S.length();
            int lenT = T.length();
            if(lenS > lenT){
                return false;
            }
    
            int[][] dp = new int[lenS+1][lenT+1];
    
            for(int i=1; i<=lenS; i++){
                for(int j=1; j<=lenT; j++){
                    if(S.charAt(i-1) == T.charAt(j-1)){
                        dp[i][j] = dp[i-1][j-1] + 1;
                    }else{
                        dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
                    }
                }
            }
    
            return dp[lenS][lenT]==lenS;
        }
    
        /**
         * 动态规划: 二维数组
         *
         * 转化为: 最长公共子序列问题
         *
         * dp[i][j]表示S以第i个字符结尾(S[0,i-1])且T以第j个字符结尾(T[0,j-1])的最长公共子序列的长度
         *
         *            { dp[i-1][j-1] + 1                  , S.charAt(i-1) == T.charAt(j-1)
         * dp[i][j] = {
         *            { Math.max(dp[i-1][j], dp[i][j-1])  , S.charAt(i-1) != T.charAt(j-1)
         *
         * @param S
         * @param T
         * @return
         */
        private boolean solution22(String S, String T){
            int lenS = S.length();
            int lenT = T.length();
            if(lenS > lenT){
                return false;
            }
    
            int[][] dp = new int[lenS+1][lenT+1];
    
            for(int i=1; i<=lenS; i++){
                for(int j=1; j<=lenT; j++){
                    if(S.charAt(i-1) == T.charAt(j-1)){
                        dp[i][j] = dp[i-1][j-1] + 1;
                    }else{
                        dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
                    }
                }
                // S[0,i-1]不是T的子序列
                if(dp[i][lenT] < i){
                    return false;
                }
            }
    
            return true;
        }
    
        /**
         * 动态规划: 一维数组(空间优化)
         *
         * 转化为: 最长公共子序列问题
         *
         * dp[j]表示T以第j个字符结尾(T[0,j-1])时的最长公共子序列的长度
         *
         *         { pre + 1                   , S.charAt(i-1) == T.charAt(j-1)
         * dp[j] = {
         *         { Math.max(dp[j-1], dp[j])  , S.charAt(i-1) != T.charAt(j-1)
         *
         * @param S
         * @param T
         * @return
         */
        private boolean solution3(String S, String T){
            int lenS = S.length();
            int lenT = T.length();
            if(lenS > lenT){
                return false;
            }
    
            int[] dp = new int[lenT+1];
    
            for(int i=1; i<=lenS; i++){
                int pre = 0;
                for(int j=1; j<=lenT; j++){
                    int tmp = dp[j];
                    if(S.charAt(i-1) == T.charAt(j-1)){
                        dp[j] = pre + 1;
                    }else{
                        dp[j] = Math.max(dp[j-1], dp[j]);
                    }
                    pre = tmp;
                }
            }
    
            return dp[lenT]==lenS;
        }
    
        /**
         * 动态规划: 一维数组(空间优化)
         * 
         * 转化为: 最长公共子序列问题
         *
         * dp[j]表示T以第j个字符结尾(T[0,j-1])时的最长公共子序列的长度
         *
         *         { pre + 1                   , S.charAt(i-1) == T.charAt(j-1)
         * dp[j] = {
         *         { Math.max(dp[j-1], dp[j])  , S.charAt(i-1) != T.charAt(j-1)
         *
         * @param S
         * @param T
         * @return
         */
        private boolean solution33(String S, String T){
            int lenS = S.length();
            int lenT = T.length();
            if(lenS > lenT){
                return false;
            }
    
            int[] dp = new int[lenT+1];
    
            for(int i=1; i<=lenS; i++){
                int pre = 0;
                for(int j=1; j<=lenT; j++){
                    int tmp = dp[j];
                    if(S.charAt(i-1) == T.charAt(j-1)){
                        dp[j] = pre + 1;
                    }else{
                        dp[j] = Math.max(dp[j-1], dp[j]);
                    }
                    pre = tmp;
                }
                // S[0,i-1]不是T的子序列
                if(dp[lenT] < i){
                    return false;
                }
            }
    
            return true;
        }
    
        /**
         * 动态规划: 二维数组
         *
         * dp[i][j]表示S[0,i-1]是否为T[0,j-1]的子序列
         *
         *            { dp[i][j-1] | dp[i-1][j-1]  , S.charAt(i-1) == T.charAt(j-1)
         * dp[i][j] = {
         *            { dp[i][j-1]                 , S.charAt(i-1) != T.charAt(j-1)
         *
         * @param S
         * @param T
         * @return
         */
        private boolean solution4(String S, String T){
            int lenS = S.length();
            int lenT = T.length();
            if(lenS > lenT){
                return false;
            }
    
            boolean[][] dp = new boolean[lenS+1][lenT+1];
            // 空串一定是T的子序列
            for(int j=0; j<=lenT; j++){
                dp[0][j] = true;
            }
    
            for(int i=1; i<=lenS; i++){
                for(int j=1; j<=lenT; j++){
                    if(S.charAt(i-1) == T.charAt(j-1)){
                        dp[i][j] = dp[i][j-1] | dp[i-1][j-1];
                    }else{
                        dp[i][j] = dp[i][j-1];
                    }
                }
            }
    
            return dp[lenS][lenT];
        }
    
        /**
         * 动态规划: 二维数组
         *
         * dp[i][j]表示S[0,i-1]是否为T[0,j-1]的子序列
         *
         *            { dp[i][j-1] | dp[i-1][j-1]  , S.charAt(i-1) == T.charAt(j-1)
         * dp[i][j] = {
         *            { dp[i][j-1]                 , S.charAt(i-1) != T.charAt(j-1)
         *
         * @param S
         * @param T
         * @return
         */
        private boolean solution44(String S, String T){
            int lenS = S.length();
            int lenT = T.length();
            if(lenS > lenT){
                return false;
            }
    
            boolean[][] dp = new boolean[lenS+1][lenT+1];
            // 空串一定是T的子序列
            for(int j=0; j<=lenT; j++){
                dp[0][j] = true;
            }
    
            for(int i=1; i<=lenS; i++){
                for(int j=1; j<=lenT; j++){
                    if(S.charAt(i-1) == T.charAt(j-1)){
                        dp[i][j] = dp[i][j-1] | dp[i-1][j-1];
                    }else{
                        dp[i][j] = dp[i][j-1];
                    }
                }
                // S[0,i-1]不是T的子序列
                if(!dp[i][lenT]){
                    return false;
                }
            }
    
            return true;
        }
    }

  

