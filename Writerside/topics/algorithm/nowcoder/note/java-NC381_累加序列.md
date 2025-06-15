# java-NC381 累加序列


    import java.math.BigInteger;
    import java.util.*;
    
    /**
     * NC381 累加序列
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param arr string字符串 
         * @return bool布尔型
         */
        public boolean AdditiveArray (String arr) {
            int len = arr.length();
    
            // 开始状态
            int max;
            for(int i=1; i<len; i++){
                for(int j=i+1; j<len; j++){
                    max = Math.max(i, j-i);
                    if((j+max<=len&&isAdditive(arr, 0, i, j, j+max)) || (j+max+1<=len&&isAdditive(arr, 0, i, j, j+max+1))){
                        return true;
                    }
                }
            }
    
            return false;
        }
    
        private boolean isAdditive(String arr, int start, int left, int right, int end){
            // 前导0
            String firstStr = arr.substring(start, left);
            if(firstStr.length()>1 && firstStr.startsWith("0")){
                return false;
            }
            // 前导0
            String secondStr = arr.substring(left, right);
            if(secondStr.length()>1 && secondStr.startsWith("0")){
                return false;
            }
            // 前导0
            String sumStr = arr.substring(right, end);
            if(sumStr.length()>1 && sumStr.startsWith("0")){
                return false;
            }
    
            BigInteger first = new BigInteger(firstStr);
            BigInteger second = new BigInteger(secondStr);
            // 是否相等
            if(first.add(second).toString().equals(sumStr)){
                // 遍历完成
                if(end == arr.length()){
                    return true;
                }else{
                    // 递归遍历
                    int max = Math.max(right-left, end-right);
                    if((end+max<=arr.length()&&isAdditive(arr, left, right, end, end+max)) || (end+max+1<=arr.length()&&isAdditive(arr, left, right, end, end+max+1))){
                        return true;
                    }
                }
            }
    
            return false;
        }
    }

  

