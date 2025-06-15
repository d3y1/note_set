# java - HJ12 字符串反转


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            String inputStr = in.nextLine();
    
            // StringBuffer reverse()
            StringBuffer inputStrBuffer = new StringBuffer(inputStr);
            inputStrBuffer.reverse();
            System.out.print(inputStrBuffer);
    
            // StringBuilder reverse()
            // StringBuilder inputStrBuilder = new StringBuilder(inputStr);
            // inputStrBuilder.reverse();
            // System.out.print(inputStrBuilder);
        }
    }

  

