# java - HJ10 字符个数统计


    import java.util.HashSet;
    import java.util.Scanner;
    import java.util.Set;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String inputLine = in.nextLine();
            int inputLen = inputLine.length();
            Set<Character> set = new HashSet<Character>();
    
            for(int i=0; i<inputLen; i++){
                set.add(inputLine.charAt(i));
            }
    
            System.out.print(set.size());
        }
    }

  

