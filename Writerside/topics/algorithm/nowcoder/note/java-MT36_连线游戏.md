# java-MT36 连线游戏


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 画图法
         *
         * 画图举例子找规律
         *
         * n=4: N1 N2 N3 N4
         * 先画一圈     n个: N1N2 N2N3 N3N4 N4N1
         * 再画中间 (n-3)个: N1N3 或 N2N4
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
    
            System.out.println(n+(n-3));
        }
    }

  

