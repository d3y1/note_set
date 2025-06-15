# java-HJ13 句子逆序


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            
            String input = in.nextLine();
    
            String[] words = input.trim().split(" ");
            int index = words.length;
    
            while(--index >= 0){
                System.out.print(words[index] + " ");
            }
    
            // System.out.print(words[index]);
        }
    }

  

