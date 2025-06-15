# java-NC361 整数转罗马数字


    import java.util.*;
    
    /**
     * NC361 整数转罗马数字
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param n int整型 
         * @return string字符串
         */
        public String ArabicToRoman (int n) {
            // return solution1(n);
            return solution2(n);
        }
    
        private final int[] values = new int[]{1000, 500, 100, 50, 10, 5, 1};
        private final HashMap<Integer,Character> map = new HashMap<Integer,Character>(){{
            put(1, 'I');
            put(5, 'V');
            put(10, 'X');
            put(50, 'L');
            put(100, 'C');
            put(500, 'D');
            put(1000, 'M');
        }};
    
        /**
         * 哈希: HashMap
         * @param n
         * @return
         */
        private String solution1(int n){
            StringBuilder sb = new StringBuilder();
            int remain = n;
            int times;
            for(int val: values){
                times = remain/val;
                remain = remain%val;
                while(times-- > 0){
                    sb.append(map.get(val));
                }
                if(remain == 0){
                    break;
                }
            }
    
            // 四连情况处理 VIIII LXXXX DCCCC | IIII XXXX CCCC
            String result = sb.toString().replace("VIIII", "IX").replace("LXXXX", "XC").replace("DCCCC", "CM").replace("IIII", "IV").replace("XXXX", "XL").replace("CCCC", "CD");
    
            return result;
        }
    
        //////////////////////////////////////////////////////////////////////////////////////////////////
    
        private final int[] arabics = new int[]{1000,900,500,400,100,90,50,40,10,9,5,4,1};
        private final String[] romans = new String[]{"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
    
        /**
         * 哈希: 数组
         * @param n
         * @return
         */
        private String solution2(int n){
            StringBuilder sb = new StringBuilder();
            int remain = n;
            int times;
            int val;
            for(int i=0; i<arabics.length; i++){
                val = arabics[i];
                times = remain/val;
                remain = remain%val;
                while(times-- > 0){
                    sb.append(romans[i]);
                }
                if(remain == 0){
                    break;
                }
            }
    
            return sb.toString();
        }
    }

  

