# java-NC351 分数到小数


    import java.util.*;
    
    /**
     * NC351 分数到小数
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param n int整型 
         * @param m int整型 
         * @return string字符串
         */
        public String frac2Dec (int n, int m) {
            // return solution1(n, m);
            return solution2(n, m);
        }
    
        /**
         * 哈希
         * @param n
         * @param m
         * @return
         */
        private String solution1(int n, int m){
            if(n == 0){
                return "0";
            }
    
            HashMap<String,Integer> map = new HashMap<>();
            // 分子
            long numerator = n;
            // 分母
            long denominator = m;
            StringBuilder sb = new StringBuilder();
    
            //  2147483647              ->     01111111111111111111111111111111 (32位)
            // -2147483648              ->     10000000000000000000000000000000 (32位)
            // 2147483647^-2147483648   ->     11111111111111111111111111111111 (32位)
            // System.out.println(Integer.toBinaryString(2147483647));
            // System.out.println(Integer.toBinaryString(-2147483648));
            // System.out.println(Integer.toBinaryString(2147483647^-2147483648));
            
            // 符号位
            long sign = (numerator)^(denominator);
            if(sign < 0){
                sb.append("-");
            }
    
            numerator = Math.abs(numerator);
            denominator = Math.abs(denominator);
            // 整数部分
            long intPart = numerator/denominator;
            sb.append(intPart);
    
            long remain = numerator%denominator;
            // 可整除
            if(remain == 0){
                return sb.toString();
            }
            // 不可整除 加小数点
            sb.append(".");
    
            String key;
            // 小数部分
            long decPart;
    
            do{
                key = remain +"/"+ denominator;
                // 循环小数
                if(map.containsKey(key)){
                    int idx = map.get(key);
                    sb.insert(idx, "(");
                    sb.append(")");
                    break;
                }
                map.put(key, sb.length());
    
                numerator = remain*10;
                decPart = numerator/denominator;
                sb.append(decPart);
                remain = numerator%denominator;
            }while(remain != 0);
    
            return sb.toString();
        }
    
        /**
         * 哈希
         * @param n
         * @param m
         * @return
         */
        private String solution2(int n, int m){
            if(n == 0){
                return "0";
            }
    
            HashMap<Long,Integer> map = new HashMap<>();
            // 分子
            long numerator = n;
            // 分母
            long denominator = m;
            StringBuilder sb = new StringBuilder();
    
            // 符号位
            long sign = (numerator)^(denominator);
            if(sign < 0){
                sb.append("-");
            }
    
            numerator = Math.abs(numerator);
            denominator = Math.abs(denominator);
            // 整数部分
            long intPart = numerator/denominator;
            sb.append(intPart);
    
            long remain = numerator%denominator;
            // 可整除
            if(remain == 0){
                return sb.toString();
            }
            // 不可整除 加小数点
            sb.append(".");
    
            Long key;
            // 小数部分
            long decPart;
    
            do{
                // 可直接将分子作为key
                key = remain;
                // 循环小数
                if(map.containsKey(key)){
                    int idx = map.get(key);
                    sb.insert(idx, "(");
                    sb.append(")");
                    break;
                }
                map.put(key, sb.length());
    
                numerator = remain*10;
                decPart = numerator/denominator;
                sb.append(decPart);
                remain = numerator%denominator;
            }while(remain != 0);
    
            return sb.toString();
        }
    }

  

