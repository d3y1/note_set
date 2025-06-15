# java-NC1 大数加法


    import java.math.BigInteger;
    import java.util.*;
    
    /**
     * NC1 大数加法
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 计算两个数之和
         * @param s string字符串 表示第一个整数
         * @param t string字符串 表示第二个整数
         * @return string字符串
         */
        public String solve (String s, String t) {
            return solution1(s, t);
            // return solution2(s, t);
            // return solution3(s, t);
        }
    
        /**
         * 模拟法
         * @param s
         * @param t
         * @return
         */
        private String solution1(String s, String t){
            if(s.equals("")){
                return t;
            }
            if(t.equals("")){
                return s;
            }
    
            return adder(s, t);
        }
    
        /**
         * 加法器
         * @param s
         * @param t
         * @return
         */
        private String adder(String s, String t){
            int sLen = s.length();
            int tLen = t.length();
            int len = Math.max(sLen, tLen);
    
            int carry = 0;
            int sum,sDigit,tDigit,digit;
            StringBuilder result = new StringBuilder();
            for(int i = 1; i <= len; i++){
                sDigit = (sLen-i >= 0) ? s.charAt(sLen-i)-'0' : 0;
                tDigit = (tLen-i >= 0) ? t.charAt(tLen-i)-'0' : 0;
                sum = sDigit + tDigit + carry;
                carry = sum / 10;
                digit = sum % 10;
                result.insert(0, digit);
            }
            if(carry > 0){
                result.insert(0, carry);
            }
    
            return result.toString();
        }
    
        /**
         * 库函数: BigInteger
         * @param s
         * @param t
         * @return
         */
        private String solution2(String s, String t){
            BigInteger bigIntegerS = new BigInteger(s);
            BigInteger bigIntegerT = new BigInteger(t);
    
            return bigIntegerS.add(bigIntegerT).toString();
        }
    
        /**
         * 模拟法: 简化
         * @param s
         * @param t
         * @return
         */
        private String solution3(String s, String t){
            int i = s.length()-1;
            int j = t.length()-1;
    
            // 进位
            int carry = 0;
            int sum,sDigit,tDigit,digit;
            StringBuilder result = new StringBuilder();
            while(i>=0 || j>=0 || carry > 0){
                sDigit = (i >= 0) ? s.charAt(i--)-'0' : 0;
                tDigit = (j >= 0) ? t.charAt(j--)-'0' : 0;
                sum = sDigit + tDigit + carry;
                carry = sum / 10;
                digit = sum % 10;
                result.insert(0, digit);
            }
            
            return result.toString();
        }
    }

  

