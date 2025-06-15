# java-NC344 Z字形输出字符串


    import java.util.*;
    
    /**
     * NC344 Z字形输出字符串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param str string字符串
         * @param k int整型
         * @return string字符串
         */
        public String zconvert (String str, int k) {
            if(k == 1){
                return str;
            }
    
            int len = str.length();
            // col
            int size = (int)Math.ceil((len-k)/(float)(k-1)) + 1;
    
            char[][] array = new char[k][size];
            for(int row=-1,col=0,i=0; i<len&&col<size; col++){
                // down 往下
                if(col%2 == 0){
                    while(row < k-1 && i<len){
                        array[++row][col] = str.charAt(i++);
                    }
                }
                // up 往上
                else{
                    while(row > 0 && i<len){
                        array[--row][col] = str.charAt(i++);
                    }
                }
            }
    
            StringBuilder sb = new StringBuilder();
            for(int i=0; i<k; i++){
                for(int j=0; j<size; j++){
                    if(Character.isLetter(array[i][j])){
                        sb.append(array[i][j]);
                    }
                }
            }
    
            return sb.toString();
        }
    }

  

