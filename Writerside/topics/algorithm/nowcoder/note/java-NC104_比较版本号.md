# java-NC104 比较版本号


    import java.util.*;
    
    /**
     * NC104 比较版本号
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 比较版本号
         * @param version1 string字符串
         * @param version2 string字符串
         * @return int整型
         */
        public int compare (String version1, String version2) {
            // return solution1(version1, version2);
            return solution2(version1, version2);
        }
    
        /**
         * 双指针
         * @param version1
         * @param version2
         * @return
         */
        private int solution1(String version1, String version2){
            int len1 = version1.length();
            int len2 = version2.length();
    
            for(int i=0,j=0; i<len1||j<len2; i++,j++){
                int num1 = 0;
                while(i<len1 && version1.charAt(i)!='.'){
                    num1 = num1*10+version1.charAt(i++)-'0';
                }
                
                int num2 = 0;
                while(j<len2 && version2.charAt(j)!='.'){
                    num2 = num2*10+version2.charAt(j++)-'0';
                }
    
                if(num1 > num2){
                    return 1;
                }
                if(num1 < num2){
                    return -1;
                }
            }
    
            return 0;
        }
    
        /**
         * 分割法
         * @param version1
         * @param version2
         * @return
         */
        private int solution2(String version1, String version2){
            String[] v1Parts = version1.split("\\.");
            String[] v2Parts = version2.split("\\.");
    
            int len1 = v1Parts.length;
            int len2 = v2Parts.length;
    
            int num1,num2;
            for(int i=0; i<len1||i<len2; i++){
                num1 = (i<len1) ? Integer.parseInt(v1Parts[i]) : 0;
                num2 = (i<len2) ? Integer.parseInt(v2Parts[i]) : 0;
                if(num1 > num2){
                    return 1;
                }
                if(num1 < num2){
                    return -1;
                }
            }
    
            return 0;
        }
    }

  

