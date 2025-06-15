# java-NC67 汉诺塔问题


    import java.util.*;
    
    /**
     * NC67 汉诺塔问题
     * @author d3y1
     */
    public class Solution {
        ArrayList<String> result = new ArrayList<String>();
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param n int整型 
         * @return string字符串ArrayList
         */
        public ArrayList<String> getSolution (int n) {
            // n from left to right
            Hanoi(n, "left", "mid", "right");
    
            return result;
        }
    
        /**
         * 递归
         * @param n
         * @param from
         * @param help
         * @param to
         */
        private void Hanoi(int n, String from, String help, String to){
            if(n > 0){
                // step1: n-1 from left to mid
                Hanoi(n-1, from, to, help);
                // step2: 1 from left to right
                result.add("move from "+from+" to "+to);
                // step3: n-1 from mid to right
                Hanoi(n-1, help, from, to);
            }
        }
    }

  

