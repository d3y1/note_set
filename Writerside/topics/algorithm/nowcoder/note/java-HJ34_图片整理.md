# java - HJ34 图片整理


    import java.util.Arrays;
    import java.util.List;
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
            char[] chars = input.toCharArray();
    
            Arrays.sort(chars);      
    
            System.out.print(chars);
        }
    }

  

