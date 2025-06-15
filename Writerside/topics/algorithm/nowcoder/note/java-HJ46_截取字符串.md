# java-HJ46 截取字符串


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                String input = in.nextLine();
                int k = in.nextInt();
                
                System.out.println(input.substring(0, k));
            }
        }
    }

  

