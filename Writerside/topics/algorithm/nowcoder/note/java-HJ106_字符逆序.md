# java-HJ106 字符逆序


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            
            String input = in.nextLine();
            StringBuilder sb = new StringBuilder(input);
            
            System.out.print(sb.reverse());
        }
    }

  

