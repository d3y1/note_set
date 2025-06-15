# java-MT14 整数加法


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法
         * @param in
         */
        private static void solution(Scanner in){
            String[] nums = in.nextLine().split(" ");
            String num0 = nums[0];
            String num1 = nums[1];
    
            if(num0.matches("\\d+") && num1.matches("\\d+")){
                StringBuilder sb = new StringBuilder();
                normalAdder(sb, num0, num1);
                System.out.println(sb);
            }else{
                System.out.println("error");
            }
        }
    
        /**
         * 两个字符串 对位相加
         * @param sb
         * @param num0
         * @param num1
         */
        private static void normalAdder(StringBuilder sb, String num0, String num1){
            int len0 = num0.length();
            int len1 = num1.length();
            int lenMin = Math.min(len0, len1);
    
            int carry = 0;
            int sum;
            int remainder;
            for(int i=1; i<=lenMin; i++){
                char ch0 = num0.charAt(len0-i);
                char ch1 = num1.charAt(len1-i);
                sum = carry + Integer.parseInt(String.valueOf(ch0)) + Integer.parseInt(String.valueOf(ch1));
                carry = sum/10;
                remainder = sum%10;
                sb.insert(0, remainder);
            }
    
            if(len0 == len1){
                if(carry > 0){
                    sb.insert(0, carry);
                }
            }else{
                if(len0 > lenMin){
                    singleAdder(sb, num0, lenMin, len0, carry);
                }
                if(len1 > lenMin){
                    singleAdder(sb, num1, lenMin, len1, carry);
                }
            }
        }
    
        /**
         * 单个字符串 多余部分与进位相加
         * @param sb
         * @param num
         * @param lenMin
         * @param lenMax
         * @param carry
         */
        private static void singleAdder(StringBuilder sb, String num, int lenMin, int lenMax, int carry){
            int sum, remainder;
            for(int i=lenMin+1; i<=lenMax; i++){
                char ch = num.charAt(lenMax-i);
                sum = carry + Integer.parseInt(String.valueOf(ch));
                carry = sum/10;
                remainder = sum%10;
                sb.insert(0, remainder);
            }
            if(carry > 0){
                sb.insert(0, carry);
            }
        }
    }

  

