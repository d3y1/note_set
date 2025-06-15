# java-HJ15 求正整数在内存中存储时1的个数


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            Integer decimal = in.nextInt();
            
            String binary = Integer.toBinaryString(decimal);
    
            int count = 0;
            for(int i=0; i<binary.length(); i++){
                if(binary.charAt(i) == '1'){
                    count++;
                }
            }
    
            System.out.print(count);
        }
    }

  

