# java-NC262 左旋转字符串


    import java.util.*;
    
    /**
     * NC262 左旋转字符串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 
         * @param str string字符串 
         * @param n int整型 
         * @return string字符串
         */
        public String LeftRotateString (String str, int n) {
            int len = str.length();
            if(n==0 || len==0){
                return str;
            }
    
            int index = n%len;
    
            return str.substring(index) + str.substring(0, index);
        }
    }

  

