# java - HJ11 数字颠倒


    import java.util.Scanner;
    
    // String chartAt()
    // public class Main {
    //     public static void main(String[] args) {
    //         Scanner in = new Scanner(System.in);
    
    //         Integer input = in.nextInt();
    //         String inputStr = input.toString();
    //         int inputStrLen = inputStr.length();
    
    //         while(--inputStrLen >= 0){
    //             System.out.print(inputStr.charAt(inputStrLen));
    //         }
    //     }
    // }
    
    // StringBuffer reverse()
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            Integer input = in.nextInt();
            StringBuffer inputStr = new StringBuffer(input.toString());
            inputStr = inputStr.reverse();
    
            System.out.print(inputStr);
        }
    }

  

