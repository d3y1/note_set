# java-HJ101 输入整型数组和排序标识，升序或降序排序


    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.Comparator;
    import java.util.List;
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
         * List.sort() - Comparator.comparingInt()
         * @param in
         */
        private static void solution1(Scanner in){
            int n = in.nextInt();
            List<Integer> valueList = new ArrayList<>();
    
            for(int i=0; i<n; i++){
                valueList.add(in.nextInt());
            }
    
            int flag = in.nextInt();
    
            // 升序
            if(flag == 0){
                valueList.sort((Comparator.comparingInt(o -> o)));
            }
            // 降序
            else if(flag == 1){
                valueList.sort((Comparator.comparingInt(o -> (int) o).reversed()));
            }
    
            for(Integer val: valueList){
                System.out.print(val+" ");
            }
        }
    
        /**
         * PriorityQueue
         * @param in
         */
        private static void solution2(Scanner in){
            int n = in.nextInt();
            int[] values = new int[n];
            for(int i=0; i<n; i++){
                values[i] = in.nextInt();
            }
    
            int flag = in.nextInt();
            // 升序
            if(flag == 0){
                PriorityQueue<Integer> queue = new PriorityQueue<>();
                for(int val: values){
                    queue.add(val);
                }
                while(queue.size()>0){
                    System.out.print(queue.poll()+" ");
                }
            }
            // 降序
            else if(flag == 1){
                PriorityQueue<Integer> queue = new PriorityQueue<>(new Comparator<Integer>(){
                    @Override
                    public int compare(Integer o1, Integer o2){
                        return o2 - o1;
                    }
                });
                //    PriorityQueue<Integer> queue = new PriorityQueue<>((o1, o2) -> o2 - o1);
                //    PriorityQueue<Integer> queue = new PriorityQueue<>(Collections.reverseOrder());
                for(int val: values){
                    queue.add(val);
                }
                while(queue.size()>0){
                    System.out.print(queue.poll()+" ");
                }
            }
        }
    }

  

