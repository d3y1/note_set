# java-MT30 序列操作


    import java.util.HashSet;
    import java.util.Scanner;
    import java.util.Stack;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
            }
        }
    
        /**
         * 模拟法: 数组
         * @param in
         */
        private static void solution1(Scanner in){
            int n = in.nextInt();
            int m = in.nextInt();
    
            int[] nums = new int[n+1];
            int[] moves = new int[m+1];
            for(int i=1; i<=m; i++){
                moves[i] = in.nextInt();
            }
    
            for(int i=m; i>=1; i--){
                int index = moves[i];
                if(nums[index] == 0){
                    System.out.println(index);
                    nums[index] = -1;
                }
            }
    
            for(int i=1; i<=n; i++){
                if(nums[i] == 0){
                    System.out.println(i);
                }
            }
        }
    
        /**
         * 模拟法: set + stack
         * @param in
         */
        private static void solution2(Scanner in){
            int n = in.nextInt();
            int m = in.nextInt();
    
            HashSet<Integer> pushSet = new HashSet<>();
            HashSet<Integer> popSet = new HashSet<>();
            Stack<Integer> stack = new Stack<>();
            int num;
            for(int i=1; i<=m; i++){
                num = in.nextInt();
                pushSet.add(num);
                stack.add(num);
            }
    
            int top;
            while(!stack.isEmpty()){
                top = stack.pop();
                if(!popSet.contains(top)){
                    System.out.println(top);
                    popSet.add(top);
                }
            }
    
            for(int i=1; i<=n; i++){
                if(!pushSet.contains(i)){
                    System.out.println(i);
                }
            }
        }
    }

  

