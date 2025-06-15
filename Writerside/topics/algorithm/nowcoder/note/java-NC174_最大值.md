# java-NC174 最大值


    import java.util.*;
    
    /**
     * NC174 最大值
     * @author d3y1
     */
    public class Solution {
        private int result = 0;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串 
         * @param k int整型 
         * @return int整型
         */
        public int maxValue (String s, int k) {
            int len = s.length();
            String sub;
            // 滑动窗口
            for(int i=0; i+k<=len; i++){
                sub = s.substring(i, i+k);
                result = Math.max(result, Integer.parseInt(sub));
            }
    
            return result;
        }
    }

  

