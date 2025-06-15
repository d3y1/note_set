# java-HJ84 统计大写字母个数


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
            
            System.out.print(input.replaceAll("[^A-Z]","").length());
        }
    
    
    
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     String input = in.nextLine();
        //     char[] chars = input.toCharArray();
    
        //     int count = 0;
        //     for(char achar: chars){
        //         // if('A'<=achar && achar<='Z'){
        //         if(Character.isUpperCase(achar)){
        //             count++;
        //         }
        //     }
    
        //     System.out.print(count);
        // }
    }

  

