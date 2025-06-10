# bit位数
https://www.nowcoder.com/practice/daf9032926614dab91ca624a7759a868

    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 位运算: 异或
         * @param in
         */
        private static void solution(Scanner in){
            int m = in.nextInt();
            int n = in.nextInt();
    
            int z = m ^ n;
            String bits = Integer.toBinaryString(z);
    
            int result = bits.replaceAll("0", "").length();
    
            System.out.println(result);
        }
    }
    

