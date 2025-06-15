# java-NC253 旋转字符串（二）


    import java.util.*;
    
    /**
     * NC253 旋转字符串（二）
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 旋转字符串
         * @param A string字符串
         * @param B string字符串
         * @return bool布尔型
         */
        public boolean solve (String A, String B) {
            return solution1(A, B);
            // return solution2(A, B);
            // return solution3(A, B);
            // return solution4(A, B);
        }
    
        /**
         * 正则
         * @param A
         * @param B
         * @return
         */
        private boolean solution1(String A, String B){
            String AA = A + A;
            int index = AA.indexOf(B);
            if(index > 0){
                return true;
            }else if(index == 0){
                // (x) => 匹配'x'并且记住匹配项 括号被称为捕获括号
                // (\\w+)\\1+ => 匹配重复字符串 如abab
                String regex = "(\\w+)\\1+";
                if(A.matches(regex)){
                    return true;
                }
            }
    
            return false;
        }
    
        /**
         * 模拟法: 字符串分割合并
         * @param A
         * @param B
         * @return
         */
        private boolean solution2(String A, String B){
            int len = A.length();
            String combine;
            for(int i = 1; i < len; i++){
                combine = A.substring(i,len)+A.substring(0,i);
                if(combine.equals(B)){
                    return true;
                }
            }
    
            return false;
        }
    
        /**
         * 字符串
         * @param A
         * @param B
         * @return
         */
        private boolean solution3(String A, String B){
            int lenA = A.length();
            int lenB = B.length();
            if(lenA != lenB){
                return false;
            }
    
            String AA = A + A;
            if(AA.substring(1, 2*lenA-1).contains(B)){
                return true;
            }
    
            return false;
        }
    
        /**
         * 字符串
         * @param A
         * @param B
         * @return
         */
        private boolean solution4(String A, String B){
            int lenA = A.length();
            int lenB = B.length();
            if(lenA != lenB){
                return false;
            }
    
            for(int i = 1; i < lenA; i++){
                if(B.endsWith(A.substring(0, i)) && B.startsWith(A.substring(i))){
                    return true;
                }
            }
    
            return false;
        }
    }

  

