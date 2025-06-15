# java-JD7 集合


    import java.util.Scanner;
    import java.util.TreeSet;
    
    /**
     * JD7 集合
     * @author d3y1
     */
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: TreeSet
         * @param in
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
            int m = in.nextInt();
    
            TreeSet<Integer> set = new TreeSet<>();
            for(int i=1; i<=n+m; i++){
                set.add(in.nextInt());
            }
    
            for(Integer value: set){
                System.out.print(value+" ");
            }
        }
    }

  

