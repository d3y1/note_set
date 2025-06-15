# java-MT37 魔法表


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()) {
                solution1(in);
                solution2(in);
            }
        }
    
        /**
         * 模拟法: 取模
         * @param in
         */
        private static void solution1(Scanner in){
            int n1 = in.nextInt();
            int n2 = in.nextInt();
    
            int clockWise = (n2-n1+360)%360;
            int antiClockWise = 360-clockWise;
    
            if(clockWise <= antiClockWise){
                System.out.println(clockWise);
            }else{
                System.out.println(-antiClockWise);
            }
        }
    
        /**
         * 模拟法: 取模
         * @param in
         */
        private static void solution2(Scanner in){
            int n1 = in.nextInt();
            int n2 = in.nextInt();
    
            int clockWise = (n2-n1+360)%360;
            int antiClockWise = (n1-n2+360)%360;
    
            if(clockWise <= antiClockWise){
                System.out.println(clockWise);
            }else{
                System.out.println(-antiClockWise);
            }
        }
    }

  

