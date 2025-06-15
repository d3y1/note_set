# java - HJ22 汽水瓶


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
    
        // bottles/2
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            
            while (in.hasNextInt()) { // 注意 while 处理多个 case
                int bottles = in.nextInt();
                if(bottles == 0){
                    break;
                }
                System.out.println(bottles/2);
            }
        }
    
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     final int BASE = 3;
        //     while (in.hasNextInt()) { // 注意 while 处理多个 case
        //         int full = 0;
        //         int empty = in.nextInt();
        //         if(empty == 0){
        //             break;
        //         }
    
        //         while(empty > 0){
        //             full += empty/BASE;
        //             empty = (empty/BASE + empty%BASE);
    
        //             if(empty == 1){
        //                 System.out.println(full);
        //                 break;
        //             }else if(empty == 2){
        //                 System.out.println(full+1);
        //                 break;
        //             }
        //         }
        //     }
        // }
    }

  

