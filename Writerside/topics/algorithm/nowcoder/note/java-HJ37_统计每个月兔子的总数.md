# java-HJ37 统计每个月兔子的总数


    import java.util.Scanner;
    
    // F(i)(总) = F(i)(幼兔1) + F(i)(幼兔2) + F(i)(成兔)
    // F(i-1)(总) = F(i-1)(幼兔1) + F(i-1)(幼兔2) + F(i-1)(成兔)
    //
    // F(i+1)(幼兔2) = F(i)(幼兔1)
    // F(i+1)(成兔) = F(i)(幼兔2) + F(i)(成兔)
    // F(i+1)(幼兔1) = F(i+1)(成兔) = F(i)(幼兔2) + F(i)(成兔)
    //
    // F(i)(幼兔2) = F(i-1)(幼兔1)
    // F(i)(成兔) = F(i-1)(幼兔2) + F(i-1)(成兔)
    //
    // F(i+1)(总) = F(i+1)(幼兔1) + F(i+1)(幼兔2) + F(i+1)(成兔)
    //            = F(i)(幼兔2) + F(i)(成兔) + F(i)(幼兔1) + F(i)(幼兔2) + F(i)(成兔)
    //            = F(i)(总) + F(i)(幼兔2) + F(i)(成兔)
    //            = F(i)(总) + F(i-1)(幼兔1) + F(i-1)(幼兔2) + F(i-1)(成兔)
    //            = F(i)(总) + F(i-1)(总)
    //
    // F(i+1)(总) = F(i)(总) + F(i-1)(总)
    public class Main {
        // 二维数组
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     int n = in.nextInt();
    
        //     int[][] rabit = new int[n+1][3];
        //     rabit[1][0] = 1;
    
        //     for(int i=2; i<=n; i++){
        //         // rabit[i][0] = rabit[i-1][2];
        //         rabit[i][1] = rabit[i-1][0];
        //         rabit[i][2] = rabit[i-1][1] + rabit[i-1][2];
        //         rabit[i][0] = rabit[i][2];
        //     }
    
        //     int result = rabit[n][0]+rabit[n][1]+rabit[n][2];
    
        //     System.out.print(result);
        // }
    
        // 递归
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            int n = in.nextInt();
    
            int result = F(n);
    
            System.out.print(result);
        }
    
        private static int F(int month){
            if(month==1 || month==2){
                return 1;
            }
                
            return F(month-1)+F(month-2);
        }
    }

  

