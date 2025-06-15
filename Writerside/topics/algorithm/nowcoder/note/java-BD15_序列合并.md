# java-BD15 序列合并


    import java.util.Comparator;
    import java.util.PriorityQueue;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: k路归并
         * @param in
         */
        private static void solution(Scanner in){
            int k = in.nextInt();
    
            int[][] factors = new int[k][8];
            for(int i=0; i<k; i++){
                for(int j=7; j>=0; j--){
                    factors[i][j] = in.nextInt();
                }
            }
            int n = in.nextInt();
    
            PriorityQueue<Node> minHeap = new PriorityQueue<>(k, Comparator.comparingLong(o -> o.val));
    
            // k路归并
            Node node;
            for(int i=0; i<k; i++){
                node = new Node(i,1,compute(factors[i], 1));
                minHeap.offer(node);
            }
    
            int count = 1;
            while(count < n){
                Node top = minHeap.poll();
                minHeap.offer(new Node(top.k, top.n+1, compute(factors[top.k], top.n+1)));
                count++;
            }
    
            System.out.println(minHeap.peek().val);
        }
    
        /**
         * 计算f(n)
         * @param factor
         * @param n
         * @return
         */
        private static long compute(int[] factor, int n){
            long value = 0L;
            for(int i=7; i>=0; i--){
                value += (int) (factor[i]*Math.pow(n,i));
            }
    
            return value;
        }
    
        private static class Node{
            // 系数factors[k]
            private int k;
            // 整数n
            private int n;
            // f(n)
            private long val;
    
            public Node(int k, int n, long val){
                this.k = k;
                this.n = n;
                this.val = val;
            }
        }
    }

  

