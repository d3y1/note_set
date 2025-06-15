# java-NC330 36进制加法


    import java.util.*;
    
    /**
     * NC330 36进制加法
     * @author d3y1
     */
    public class Solution {
        private final int RADIX  = 36;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param A string字符串
         * @param B string字符串
         * @return string字符串
         */
        public String thirtysixAdd (String A, String B) {
            String digits = "0123456789abcdefghijklmnopqrstuvwxyz";
            HashMap<Character, Integer> charNumMap = new HashMap<>();
            HashMap<Integer, Character> numCharMap = new HashMap<>();
            for(int i=0; i<RADIX; i++){
                charNumMap.put(digits.charAt(i), i);
                numCharMap.put(i, digits.charAt(i));
            }
    
            int lenA = A.length();
            int lenB = B.length();
    
            int carry = 0;
            int sum;
            int digit,digitA,digitB;
            StringBuilder sb = new StringBuilder();
            for(int i=lenA-1,j=lenB-1; i>=0||j>=0||carry>0; i--,j--){
                digitA = (i>=0)?charNumMap.get(A.charAt(i)):0;
                digitB = (j>=0)?charNumMap.get(B.charAt(j)):0;
                
                sum = digitA + digitB + carry;
                digit = sum % RADIX;
                carry = sum / RADIX;
    
                // sb.insert(0, numCharMap.get(digit)) => 超时
                sb.append(numCharMap.get(digit));
            }
    
            return sb.reverse().toString();
        }
    }

  

