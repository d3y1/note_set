# java-ZJ24 机器人跳跃问题


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                // solution2(in);
            }
        }
    
        /**
         * 模拟法: 数学公式倒推
         * 三种情形 可合为一
         */
        private static void solution1(Scanner in){
            int N = in.nextInt();
            int[] H = new int[N+1];
            int[] E = new int[N+1];
    
            for(int i=1; i<=N; i++){
                H[i] = in.nextInt();
            }
    
            for(int i=N; i>0; i--){
                // E[i]<H[i] => E[i-1]<H[i], E[i-1]-(H[i]-E[i-1])=E[i] => E[i-1] = Math.ceil((E[i]+H[i])/2)
                // E[i]>H[i] => E[i-1]>H[i], E[i-1]+(E[i-1]-H[i])=E[i] => E[i-1] = Math.ceil((E[i]+H[i])/2)
                // E[i]=H[i] => E[i-1]=H[i], E[i-1]=E[i] => 2E[i-1]=E[i]+H[i] => E[i-1] = Math.ceil((E[i]+H[i])/2)
                E[i-1] = (int) Math.ceil((E[i]+H[i])/2.0);
            }
    
            System.out.println(E[0]);
        }
        
    
        /**
         * 模拟法: 数学公式倒推
         */
        private static void solution2(Scanner in){
            int N = in.nextInt();
            int[] H = new int[N+1];
            int[] E = new int[N+1];
    
            for(int i=1; i<=N; i++){
                H[i] = in.nextInt();
            }
    
            // E[N-1] = (int) Math.ceil(H[N]/2.0) -> 可合并
            for(int i=N; i>0; i--){
                // E[i]<H[i] => E[i-1]<H[i], E[i-1]-(H[i]-E[i-1])=E[i] => E[i-1] = Math.ceil((E[i]+H[i])/2)
                if(E[i] < H[i]){
                    E[i-1] = (int) Math.ceil((E[i]+H[i])/2.0);
                }
                // E[i]>H[i] => E[i-1]>H[i], E[i-1]+(E[i-1]-H[i])=E[i] => E[i-1] = Math.ceil((E[i]+H[i])/2)
                else if(E[i] > H[i]){
                    E[i-1] = (int) Math.ceil((E[i]+H[i])/2.0);
                }else{
                    E[i-1] = H[i];
                }
            }
    
            System.out.println(E[0]);
        }
    }

  

