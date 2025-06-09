# 验证IP地址
https://www.nowcoder.com/practice/55fb3c68d08d46119f76ae2df7566880

    import java.util.*;
    
    /**
     * NC113 验证IP地址
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 验证IP地址
         * @param IP string字符串 一个IP地址字符串
         * @return string字符串
         */
        public String solve (String IP) {
            // return solution1(IP);
            return solution2(IP);
        }
    
        /**
         * 分段法
         * @param IP
         * @return
         */
        private String solution1(String IP){
            if(IP.contains(".")){
                if(isIPv4(IP)){
                    return "IPv4";
                }
            }
            if(IP.contains(":")){
                if(isIPv6(IP)){
                    return "IPv6";
                }
            }
    
            return "Neither";
        }
    
        /**
         * 是否IPv4
         * @param IP
         * @return
         */
        private boolean isIPv4(String IP){
            String[] parts = IP.split("\\.", -1);
            if(parts.length != 4){
                return false;
            }
            // String regex = "\\d{1,3}";
            String regex = "[0-9]{1,3}";
            for(String part: parts){
                if(!part.matches(regex)){
                    return false;
                }
                if(part.length()>1 && part.startsWith("0")){
                    return false;
                }
                if(255 < Integer.parseInt(part)){
                    return false;
                }
            }
    
            return true;
        }
    
        /**
         * 是否IPv6
         * @param IP
         * @return
         */
        private boolean isIPv6(String IP){
            String[] parts = IP.split(":", -1);
            if(parts.length != 8){
                return false;
            }
            String regex = "[0-9a-fA-F]{1,4}";
            for(String part: parts){
                if(!part.matches(regex)){
                    return false;
                }
            }
    
            return true;
        }
    
        /**
         * 正则表达式
         * @param IP
         * @return
         */
        private String solution2(String IP){
            String regexIPv4 = "(([0-9]|[1-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])";
            String regexIPv6 = "(([0-9a-fA-F]{1,4}):){7}([0-9a-fA-F]{1,4})";
    
            if(IP.matches(regexIPv4)){
                return "IPv4";
            }
            if(IP.matches(regexIPv6)){
                return "IPv6";
            }
    
            return "Neither";
        }
    }
    

