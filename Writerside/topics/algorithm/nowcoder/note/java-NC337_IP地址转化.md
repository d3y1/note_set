# java-NC337 IP地址转化


    import java.util.*;
    
    /**
     * NC337 IP地址转化
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param ip string字符串 
         * @return string字符串
         */
        public String IPtoNum (String ip) {
            return solution1(ip);
            // return solution2(ip);
        }
    
        /**
         * 进制: 进制转换
         * @param ip
         * @return
         */
        private String solution1(String ip){
            String[] ipParts = ip.split("\\.");
    
            StringBuilder sb = new StringBuilder();
            for(int i=0; i<4; i++){
                sb.append(String.format("%08d", Integer.parseInt(Integer.toBinaryString(Integer.parseInt(ipParts[i])))));
            }
    
            return String.valueOf(Long.parseLong(sb.toString(), 2));
        }
    
    
        /**
         * 进制: 256进制
         * @param ip
         * @return
         */
        private String solution2(String ip){
            String[] ipParts = ip.split("\\.");
            Long result = 0L;
    
            for(int i=3; i>=0; i--){
                result += Long.parseLong(ipParts[i])<<((3-i)*8);
            }
    
            return String.valueOf(result);
        }
    }

  

