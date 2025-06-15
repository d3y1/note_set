# java-QQ4 游戏任务标记


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                // solution1(in);
                solution2(in);
            }
        }
    
        /**
         * 模拟法: 位运算
         * 简化
         * @param in
         */
        private static void solution2(Scanner in){
            int setupID = in.nextInt();
            int checkID = in.nextInt();
    
            int result;
            if((1<=setupID&&setupID<=1024) && (1<=checkID&&checkID<=1024)){
                int[] tasks = new int[32];
                int m,n;
    
                // unset
    //            m = (setupID-1)>>5;
    //            n = (setupID-1)&31;
    //            tasks[m] &= ~(1<<n);
                
                // setup
                m = (setupID-1)>>5;
                n = (setupID-1)&31;
                tasks[m] |= (1<<n);
    
                // check
                m = (checkID-1)>>5;
                n = (checkID-1)&31;
                result = (tasks[m]&(1<<n))>>>n;
            }else{
                result = -1;
            }
    
            System.out.println(result);
        }
    
        /**
         * 模拟法: 位运算
         * @param in
         */
        private static void solution1(Scanner in){
            int setupID = in.nextInt();
            int checkID = in.nextInt();
    
            int result;
            if((1<=setupID&&setupID<=1024) && (1<=checkID&&checkID<=1024)){
                int[] tasks = new int[32];
                int m,n;
    
                // setup
                m = (setupID-1)/32;
                n = (setupID-1)%32;
                tasks[m] |= (1<<n);
    
                // check
                m = (checkID-1)/32;
                n = (checkID-1)%32;
                result = (tasks[m]&(1<<n))>>>n;
            }else{
                result = -1;
            }
    
            System.out.println(result);
        }
    }

  

