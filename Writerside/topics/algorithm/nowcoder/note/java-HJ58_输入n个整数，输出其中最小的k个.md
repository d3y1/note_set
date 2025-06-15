# java-HJ58 输入n个整数，输出其中最小的k个


    import java.util.Arrays;
    import java.util.PriorityQueue;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
            }
        }
    
        /**
         * 最小堆 PriorityQueue
         * @param in
         */
        private static void solution1(Scanner in){
            int n = in.nextInt();
            int k = in.nextInt();
    
            PriorityQueue<Integer> queue = new PriorityQueue<>();
            for(int i=1; i<=n; i++){
                queue.add(in.nextInt());
            }
    
            for(int i=1; i<=k; i++){
                System.out.print(queue.poll()+" ");
            }
        }
    
    
        /**
         * 数组
         * @param in
         */
        private static void solution2(Scanner in){
            int n = in.nextInt();
            int k = in.nextInt();
    
            int[] nums = new int[n];
            for(int i=0; i<n; i++){
                nums[i] = in.nextInt();
            }
            Arrays.sort(nums);
    
            for(int i=0; i<k; i++){
                System.out.print(nums[i]+" ");
            }
        }
    }

  

