# java-MT1 最大差值


    import java.util.*;
    
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 
         * @param A int整型一维数组 
         * @param n int整型 
         * @return int整型
         */
        public int getDis (int[] A, int n) {
            int result = 0;
            int min = A[0];
            for(int i=0; i<n; i++){
                min = Math.min(min, A[i]);
                result = Math.max(result, A[i]-min);
            }
    
            return result;
        }
    }

  

