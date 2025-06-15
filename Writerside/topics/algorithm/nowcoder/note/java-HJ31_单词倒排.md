# java - HJ31 单词倒排


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
            String[] words = input.split("[^A-Za-z]");
    
            int index = words.length;
            while(index > 0){
                System.out.print(words[--index]+" ");
            }
        }
    
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     String input = in.nextLine();
        //     char[] chars = input.toCharArray();
    
        //     for(int i=0; i<chars.length; i++){
        //         if(!(('A'<=chars[i]&&chars[i]<='Z') || ('a'<=chars[i]&&chars[i]<='z'))){
        //             chars[i] = ' ';
        //         }
        //     }
    
        //     input = String.valueOf(chars);
        //     input = input.replaceAll("\\s+", " ");
        //     String[] words = input.split(" ");
    
        //     int index = words.length;
        //     while(index > 0){
        //         System.out.print(words[--index]+" ");
        //     }
        // }
    }

  

