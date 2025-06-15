# java-HJ40 统计字符


    import java.util.HashMap;
    import java.util.Map;
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
    
        private static final int SIZE = 4;
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
            char[] chars = input.toCharArray();
            int[] count = new int[SIZE];
    
            for(char aChar: chars){
                if(('A'<=aChar && aChar<='Z') || ('a'<=aChar && aChar<='z')){
                    count[0]++;
                }else if(' ' == aChar){
                    count[1]++;
                }else if('0'<=aChar && aChar<='9'){
                    count[2]++;
                }else{
                    count[3]++;
                }
            }
    
            for(int i=0; i<SIZE; i++){
                System.out.println(count[i]);
            }
        }
    }

  

