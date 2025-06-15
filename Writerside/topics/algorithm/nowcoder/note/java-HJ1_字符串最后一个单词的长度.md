# java - HJ1 字符串最后一个单词的长度


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String inputStr = in.nextLine();
    
            int result = getLastWordLength(inputStr);
    
            System.out.println(result);
        }
    
        private static int getLastWordLength(String inputStr) {
            // if (inputStr == null || inputStr.length() == 0) {
            //     return 0;
            // }
    
            String[] words = inputStr.split(" ");
            // if(words.length == 0){
            //     return 0;
            // }
            String word = words[words.length - 1];
    
            return word.length();
        }
    }

  

