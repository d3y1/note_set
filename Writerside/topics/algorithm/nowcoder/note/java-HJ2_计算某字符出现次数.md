# java - HJ2 计算某字符出现次数


    import java.util.Scanner;
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        // replaceAll()
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String inputStr = in.nextLine().toLowerCase();
            String character = in.nextLine().toLowerCase();
    
            int inputLen = inputStr.length();
            int lastLen = inputStr.replaceAll(character, "").length();
    
            System.out.println(inputLen-lastLen);
        }
    
    
        // pattern.matcher()
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     String inputStr = in.nextLine().toLowerCase();
        //     String character = in.nextLine().toLowerCase();
        //     int count = 0;
    
        //     Pattern pattern = Pattern.compile(character);
        //     Matcher matcher = pattern.matcher(inputStr);
    
        //     while(matcher.find()){
        //         count++;
        //     }
    
        //     System.out.println(count);
        // }
    
    
        // indexOf()
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     String inputStr = in.nextLine().toLowerCase();
        //     String character = in.nextLine().toLowerCase();
        //     int count = 0;
    
        //     int index = inputStr.indexOf(character);
    
        //     while (index != -1) {
        //         count++;
        //         index = inputStr.indexOf(character, index+1);
        //     }
    
        //     System.out.println(count);
        // }
    }

  

