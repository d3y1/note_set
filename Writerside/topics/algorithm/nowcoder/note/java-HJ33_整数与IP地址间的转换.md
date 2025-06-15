# java-HJ33 整数与IP地址间的转换


    import java.util.Scanner;
    
    /**
     * HJ33 整数与IP地址间的转换
     * @author d3y1
     */
    public class Main {
        public static void main(String[] args) {
            // solution1();
            solution2();
        }
    
        /**
         * 字符串
         */
        private static void solution1(){
            Scanner in = new Scanner(System.in);
    
            String ipAddr = in.nextLine().trim();
            String ipNumber = in.nextLine().trim();
    
            System.out.println(ipAddrToNumber(ipAddr));
            System.out.println(ipNumberToAddr(ipNumber));
        }
    
        /**
         * IP地址 -> 10进制的IP地址
         * 
         * 256进制 -> 2进制 -> 10进制
         * 
         * @param ipAddr
         * @return
         */
        private static String ipAddrToNumber(String ipAddr){
            String[] parts = ipAddr.split("\\.");
            StringBuilder sb = new StringBuilder();
            String binStr;
            int len;
            for(String part: parts){
                binStr = Integer.toBinaryString(Integer.parseInt(part));
                len = binStr.length();
                for(int i=1; i<=8-len; i++){
                    sb.append(0);
                }
                sb.append(binStr);
            }
    
            // Long number = 0L;
            // for(char ch: sb.toString().toCharArray()){
            //     number = (number<<1) + Integer.valueOf(String.valueOf(ch));
            // }
    
            return String.valueOf(Long.parseLong(sb.toString(), 2));
        }
    
        /**
         * 10进制的IP地址 -> IP地址
         * 
         * 10进制 -> 2进制 -> 256进制
         * 
         * @param ipNumber
         * @return
         */
        private static String ipNumberToAddr(String ipNumber){
            String binStr = Long.toBinaryString(Long.parseLong(ipNumber));
            int len = binStr.length();
            StringBuilder sb = new StringBuilder();
            for(int i=1; i<=32-len; i++){
                sb.append(0);
            }
            sb.append(binStr);
    
            StringBuilder ipAddr = new StringBuilder();
            String ipBinStr = sb.toString();
            String part;
            int val;
            for(int i=0; i<32; i+=8){
                part = ipBinStr.substring(i, i+8);
                // val = 0;
                // for(char ch: part.toCharArray()){
                //     val = (val<<1) + Integer.valueOf(String.valueOf(ch));
                // }
                val = Integer.parseInt(part, 2);
                ipAddr.append(val);
                ipAddr.append(".");
            }
    
            return ipAddr.substring(0, ipAddr.length()-1);
        }
    
        /**
         * 字符串
         */
        private static void solution2(){
            Scanner in = new Scanner(System.in);
    
            String ipAddr = in.nextLine().trim();
            String ipNumber = in.nextLine().trim();
    
            System.out.println(AddrToNumber(ipAddr));
            System.out.println(NumberToAddr(ipNumber));
        }
    
        /**
         * IP地址 -> 10进制的IP地址
         * 
         * 256进制 -> 10进制 (直接转换 不用经过2进制)
         * 
         * @param ipAddr
         * @return
         */
        private static String AddrToNumber(String ipAddr){
            String[] parts = ipAddr.split("\\.");
            Long number = 0L;
            for(String part: parts){
                number = number*256 + Integer.parseInt(part);
            }
    
            return String.valueOf(number);
        }
    
        /**
         * 10进制的IP地址 -> IP地址
         * 
         * 10进制 -> 256进制 (直接转换 不用经过2进制)
         * 
         * @param ipNumber
         * @return
         */
        private static String NumberToAddr(String ipNumber){
            Long number = Long.parseLong(ipNumber);
            StringBuilder sb = new StringBuilder();
            for(int i=1; i<=4; i++){
                sb.insert(0, number%256+".");
                number /= 256;
            }
    
            return sb.substring(0, sb.length()-1);
        }
    }

  

