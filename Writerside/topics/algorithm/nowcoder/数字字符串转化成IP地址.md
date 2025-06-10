# 数字字符串转化成IP地址
https://www.nowcoder.com/practice/ce73540d47374dbe85b3125f57727e1e

    import java.util.*;
    
    /**
     * NC20 数字字符串转化成IP地址
     * @author d3y1
     */
    public class Solution {
        private ArrayList<String> result = new ArrayList<>();
        private int len;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串
         * @return string字符串ArrayList
         */
        public ArrayList<String> restoreIpAddresses (String s) {
            len = s.length();
            if(len<4 || 12<len){
                return new ArrayList<>();
            }
            
            dfs(s, 0, new ArrayList<>(), 0);
    
            return result;
        }
    
        /**
         * 回溯: 递归
         * @param s
         * @param index
         * @param ip
         * @param ipParts
         */
        private void dfs(String s, int index, List<String> ip, int ipParts){
            if(ipParts==4 && index==s.length()){
                result.add(String.join(".", ip));
                return;
            }
            if(ipParts > 4){
                return;
            }
    
            // ip段长度 3种情况(1 2 3)
            for(int i = 1; i <= 3; i++){
                if(index+i <= len){
                    String part = s.substring(index, index+i);
                    if(isValid(part)){
                        ip.add(part);
                        dfs(s, index+i, ip, ipParts+1);
                        ip.remove(ipParts);
                    }
                }
            }
        }
    
        /**
         * 是否合法(ip段)
         * @param part
         * @return
         */
        private boolean isValid(String part){
            if(part.length()>1 && part.startsWith("0")){
                return false;
            }
    
            if(Integer.parseInt(part) > 255){
                return false;
            }
    
            return true;
        }
    }
    

