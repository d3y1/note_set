# java-MT26 改考卷


    import java.util.Arrays;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: 最大组人数小于等于其他所有组人数之和即可
         * @param in
         */
        private static void solution(Scanner in){
            int N = in.nextInt();
    
            int[] groups = new int[N];
            for(int i=0; i<N; i++){
                groups[i] = in.nextInt();
            }
    
            Arrays.sort(groups);
    
            int[] sum = new int[N];
            sum[0] = groups[0];
            for(int i=1; i<N; i++){
                sum[i] = sum[i-1] + groups[i];
            }
    
            if(groups[N-1] > sum[N-2]){
                System.out.println("No");
            }else{
                System.out.println("Yes");
            }
        }
    }

  

