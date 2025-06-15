# java-NC301 最大数字交换


    import java.util.*;
    
    /**
     * NC301 最大数字交换
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param num string字符串
         * @return string字符串
         */
        public String maximumSwap (String num) {
            return solution1(num);
            // return solution2(num);
        }
    
        /**
         * 贪心
         * @param num
         * @return
         */
        private String solution1(String num){
            int n = num.length();
            if(n == 1){
                return num;
            }
    
            char[] digits = num.toCharArray();
    
            // rMaxIndex[i]: i右侧最大值索引
            int[] rMaxIndex = new int[n];
            rMaxIndex[n-2] = n-1;
            // 最大值索引
            int maxIndex = n-1;
            // 从右往左
            for(int i=n-2; i>0; i--){
                // 大于 保存当前处最大值索引(maxIndex等于i)
                // 等于 保存最右侧最大值索引(maxIndex不用变)
                if(digits[i] > digits[maxIndex]){
                    maxIndex = i;
                }
                rMaxIndex[i-1] = maxIndex;
            }
    
            StringBuilder sb = new StringBuilder(num);
            for(int i=0; i<n-1; i++){
                if(digits[i] < digits[rMaxIndex[i]]){
                    sb.setCharAt(i, digits[rMaxIndex[i]]);
                    sb.setCharAt(rMaxIndex[i], digits[i]);
                    break;
                }
            }
    
            return sb.toString();
        }
    
        /**
         * 排序+贪心
         * @param num
         * @return
         */
        private String solution2(String num){
            int n = num.length();
            if(n == 1){
                return num;
            }
    
            char[] digits = num.toCharArray();
            char[] numChs = num.toCharArray();
    
            // 升序
            Arrays.sort(numChs);
            // 降序
            char[] descDigits = new StringBuilder(new String(numChs)).reverse().toString().toCharArray();
    
            StringBuilder sb = new StringBuilder(num);
            for(int i=0; i<n-1; i++){
                if(digits[i] != descDigits[i]){
                    int index = num.lastIndexOf(descDigits[i]);
                    sb.setCharAt(i, descDigits[i]);
                    sb.setCharAt(index, digits[i]);
                    break;
                }
            }
    
            return sb.toString();
        }
    }

  

