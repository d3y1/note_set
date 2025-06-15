# java-NC142 最长重复子串


    import java.util.*;
    
    /**
     * NC142 最长重复子串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param a string字符串 待计算字符串
         * @return int整型
         */
        public int solve (String a) {
            int len = a.length();
    
            // 滑动窗口
            for(int gap=len/2; gap>0; gap--){
                for(int j=0; j+2*gap<=len; j++){
                    if(a.substring(j, j+gap).equals(a.substring(j+gap, j+2*gap))){
                        return gap*2;
                    }
                }
            }
    
            return 0;
        }
    }

  

