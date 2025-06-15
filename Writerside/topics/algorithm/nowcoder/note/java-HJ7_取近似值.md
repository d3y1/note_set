# java-HJ7 取近似值


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                double num = in.nextDouble();
                System.out.println((int)(num+0.5));
            }
        }
        
        
    
    //    /**
    //     * Math.round()
    //     * @param args
    //     */
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        while (in.hasNext()){
    //            double num = in.nextDouble();
    //            System.out.println(Math.round(num));
    //        }
    //    }
    }

  

