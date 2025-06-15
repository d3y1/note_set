# java - HJ4 字符串分隔


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            String inputStr = in.nextLine();
            int inputStrLen = inputStr.length();
            int wordLen = 8;
            int beginIndex = 0;
    
            while(beginIndex+wordLen < inputStrLen){
                System.out.println(inputStr.substring(beginIndex, beginIndex+wordLen));
                beginIndex += 8;
            }
    
            System.out.printf(inputStr.substring(beginIndex));
            for(int i=beginIndex+wordLen-inputStrLen; i>0; i--){
                System.out.printf("0");
            }
        }
    }

  

