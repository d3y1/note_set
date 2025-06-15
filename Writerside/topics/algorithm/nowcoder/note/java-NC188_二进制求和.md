# java-NC188 二进制求和


    import java.math.BigInteger;
    import java.util.*;
    
    /**
     * NC188 二进制求和
     * @author d3y1
     */
    public class Solution {
        // 进制
        private final int RADIX = 2;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param A string字符串
         * @param B string字符串
         * @return string字符串
         */
        public String binaryAdd (String A, String B) {
            return solution1(A, B);
            // return solution2(A, B);
        }
    
        /**
         * 模拟法
         * @param A
         * @param B
         * @return
         */
        private String solution1(String A, String B){
            int carry = 0;
            int sum,digitA,digitB,digit;
            StringBuilder result = new StringBuilder();
    
            int i = A.length()-1;
            int j = B.length()-1;
            while(i>=0 || j>=0 || carry>0){
                digitA = (i>=0)?A.charAt(i--)-'0':0;
                digitB = (j>=0)?B.charAt(j--)-'0':0;
                sum = digitA + digitB + carry;
                digit = sum % RADIX;
                carry = sum / RADIX;
                result.insert(0, digit);
            }
    
            return result.toString();
        }
    
        /**
         * 库函数: BigInteger
         * @param A
         * @param B
         * @return
         */
        private String solution2(String A, String B){
            BigInteger bigIntegerA = new BigInteger(A, RADIX);
            BigInteger bigIntegerB = new BigInteger(B, RADIX);
    
            return bigIntegerA.add(bigIntegerB).toString(RADIX);
        }
    }

  

