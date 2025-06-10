# eli和字符串
https://www.nowcoder.com/practice/0259119d24ca40b897218f09137e4be2

    import java.util.*;
    
    /**
     * NC400 eli和字符串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param str string字符串 
         * @param k int整型 
         * @return int整型
         */
        public int eliStr (String str, int k) {
            return solution(str, k);
        }
    
        /**
         * 双指针
         * @param str
         * @param k
         * @return
         */
        private int solution(String str, int k){
            int len = str.length();
            int[] count = new int[26];
            char chR,chL;
            int result = Integer.MAX_VALUE;
            for(int i=0,j=0; j<len; j++){
                chR = str.charAt(j);
                count[chR-'a']++;
                while(count[chR-'a'] == k){
                    result = Math.min(result, j-i+1);
                    chL = str.charAt(i);
                    count[chL-'a']--;
                    i++;
                }
            }
    
            if(result == Integer.MAX_VALUE){
                result = -1;
            }
    
            return result;
        }
    }
    

