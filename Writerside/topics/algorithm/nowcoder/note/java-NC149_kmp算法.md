# java-NC149 kmp算法


    import java.util.*;
    
    /**
     * NC149 kmp算法
     * @author d3y1
     */
    public class Solution {
        private int result = 0;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 计算模板串S在文本串T中出现了多少次
         * @param S string字符串 模板串
         * @param T string字符串 文本串
         * @return int整型
         */
        public int kmp (String S, String T) {
            KMP_MATCHER(T, S);
    
            return result;
        }
    
        public int[] COMPUTE_PREFIX_FUNCTION(String S){
            int m = S.length();
            char[] charsS = S.toCharArray();
            int[] prefix = new int[m];
            prefix[0] = 0;
            int k = 0;
            for(int q=2; q<=m; q++){
                while (k>0 && charsS[k]!=charsS[q-1]){
                    k = prefix[k];
                }
                if(charsS[k] == charsS[q-1]){
                    k = k+1;
                }
                prefix[q-1] = k;
            }
    
            return prefix;
        }
    
        /**
         * KMP算法
         *
         *《INTRODUCTION TO ALGORITHMS》THIRD EDITION.
         *
         * @param T
         * @param S
         */
        public void KMP_MATCHER(String T, String S){
            int n = T.length();
            int m = S.length();
            char[] charsT = T.toCharArray();
            char[] charsS = S.toCharArray();
            int[] prefix = COMPUTE_PREFIX_FUNCTION(S);
            int q = 0;
            for(int i=1; i<=n; i++){
                while (q>0 && charsS[q]!=charsT[i-1]){
                    q = prefix[q-1];
                }
                if(charsS[q] == charsT[i-1]){
                    q = q+1;
                }
                if(q == m){
                    result++;
                    q = prefix[q-1];
                }
            }
        }
    }

  

