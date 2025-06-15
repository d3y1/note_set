# java-NC35 编辑距离(二)


    import java.util.*;
    
    /**
     * NC35 编辑距离(二)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * min edit cost
         * @param str1 string字符串 the string
         * @param str2 string字符串 the string
         * @param ic int整型 insert cost
         * @param dc int整型 delete cost
         * @param rc int整型 replace cost
         * @return int整型
         */
        public int minEditCost (String str1, String str2, int ic, int dc, int rc) {
            return solution1(str1, str2, ic, dc, rc);
            // return solution2(str1, str2, ic, dc, rc);
        }
    
        /**
         * 动态规划: 二维数组
         *
         * dp[i][j]表示字符串str1的前i个字符与字符串str2的前j个字符相同所需要的最小编辑代价
         *
         * @param str1
         * @param str2
         * @param ic
         * @param dc
         * @param rc
         * @return
         */
        private int solution1(String str1, String str2, int ic, int dc, int rc){
            int len1 = str1.length();
            int len2 = str2.length();
    
            int[][] dp = new int[len1+1][len2+1];
    
            // 初始化
            for(int i=0; i<=len1; i++){
                dp[i][0] = i*dc;
            }
            for(int j=0; j<=len2; j++){
                dp[0][j] = j*ic;
            }
    
            for(int i=1; i<=len1; i++){
                for(int j=1; j<=len2; j++){
                    // case 1
                    if(str1.charAt(i-1) == str2.charAt(j-1)){
                        dp[i][j] = dp[i-1][j-1];
                    }
                    // case 2
                    else{
                        // str1 => str2
                        // delete:  dp[i-1][j]+dc   (最先delete)
                        // insert:  dp[i][j-1]+ic   (最后insert)
                        // replace: dp[i-1][j-1]+rc (直接replace)
                        dp[i][j] = Math.min(Math.min(dp[i-1][j]+dc, dp[i][j-1]+ic), dp[i-1][j-1]+rc);
                    }
                }
            }
    
            return dp[len1][len2];
        }
    
        /**
         * 动态规划: 一维数组
         *
         * dp[j]表示编辑成字符串str2的前j个字符所需要的最小编辑代价
         *
         * @param str1
         * @param str2
         * @param ic
         * @param dc
         * @param rc
         * @return
         */
        private int solution2(String str1, String str2, int ic, int dc, int rc){
            int len1 = str1.length();
            int len2 = str2.length();
    
            int[] dp = new int[len2+1];
    
            // 初始化
            for(int j=0; j<=len2; j++){
                dp[j] = j*ic;
            }
    
            for(int i=1; i<=len1; i++){
                int pre = dp[0];
                dp[0] = i*dc;
                for(int j=1; j<=len2; j++){
                    // tmp -> dp[i-1][j]
                    int tmp = dp[j];
                    // case 1
                    if(str1.charAt(i-1) == str2.charAt(j-1)){
                        dp[j] = pre;
                    }
                    // case 2
                    else{
                        // str1 => str2
                        // delete:  tmp+dc   (最先delete)
                        // insert:  dp[j-1]+ic   (最后insert)
                        // replace: pre+rc (直接replace)
                        // dp[j-1] -> dp[i][j-1]
                        dp[j] = Math.min(Math.min(tmp+dc, dp[j-1]+ic), pre+rc);
                    }
                    // pre -> dp[i-1][j-1]
                    pre = tmp;
                }
            }
    
            return dp[len2];
        }
    }

  

