# java-HJ30 字符串合并处理


    import java.util.Arrays;
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
    
            // 1. 前后合并
            String str = in.nextLine().replaceAll(" ", "");
    
            // 2. 奇偶排序
            StringBuilder odd = new StringBuilder();
            StringBuilder even = new StringBuilder();
            for(int i=1; i<=str.length(); i++){
                char ch = str.charAt(i-1);
                if(i%2 == 0){
                    even.append(ch);
                }else{
                    odd.append(ch);
                }
            }
    
            char[] oddArray = odd.toString().toCharArray();
            char[] evenArray = even.toString().toCharArray();
    
            Arrays.sort(oddArray);
            Arrays.sort(evenArray);
            
            // 3. 字符转换
            int oddLen = oddArray.length;
            int evenLen = evenArray.length;
            StringBuilder result = new StringBuilder();
            for(int i=0; i<evenLen; i++){
                result.append(transfer(oddArray[i]));
                result.append(transfer(evenArray[i]));
            }
    
            // 特殊情况 奇偶不等
            if(oddLen > evenLen){
                result.append(transfer(oddArray[oddLen-1]));
            }
    
            System.out.println(result);
        }
    
        /**
         * 字符转换
         * @param ch
         * @return
         */
        private static Character transfer(char ch){
            if(String.valueOf(ch).matches("[0-9A-Fa-f]")){
                // 16进制 -> 10进制 -> 2进制
                String chBinary = String.format("%04d", Integer.parseInt(Integer.toBinaryString(Integer.parseInt(String.valueOf(ch), 16))));
                // 翻转
                String chReverse = new StringBuilder(chBinary).reverse().toString();
    
                // 2进制 -> 10进制 -> 16进制(大写)
                return Integer.toHexString(Integer.parseInt(chReverse, 2)).toUpperCase().charAt(0);
            }
    
            return ch;
        }
    }

  

