# java-NC68 跳台阶


    import java.util.*;
    
    /**
     * NC68 跳台阶
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param number int整型 
         * @return int整型
         */
        public int jumpFloor (int number) {
            return solution1(number);
            // return solution2(number);
        }
    
        /**
         * 递归
         * @param number
         * @return
         */
        private int solution1(int number){
            if(number == 0){
                return 1;
            }
            if(number == 1){
                return 1;
            }
    
            return solution1(number-1)+solution1(number-2);
        }
    
        /**
         * 迭代
         * @param number
         * @return
         */
        private int solution2(int number){
            if(number == 0){
                return 1;
            }
            if(number == 1){
                return 1;
            }
    
            int f1 = 1;
            int f2 = 1;
            int result = 0;
            for(int i=2; i<=number; i++){
                result = f1+f2;
                f1 = f2;
                f2 = result;
            }
    
            return result;
        }
    }

  

