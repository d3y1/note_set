# java-HJ80 整型数组合并


    import java.util.Arrays;
    import java.util.HashSet;
    import java.util.Scanner;
    import java.util.TreeSet;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * tree
         * @param args
         */
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            TreeSet<Integer> set = new TreeSet<>();
    
            int m = in.nextInt();
            for(int i=1; i<=m; i++){
                set.add(in.nextInt());
            }
    
            int n = in.nextInt();
            for (int i = 1; i <=n ; i++) {
                set.add(in.nextInt());
            }
    
            for(Integer num: set){
                System.out.print(num);
            }
        }
    
    //    /**
    //     * HashSet
    //     */
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        HashSet<Integer> set = new HashSet<>();
    //
    //        int m = in.nextInt();
    //        for(int i=1; i<=m; i++){
    //            set.add(in.nextInt());
    //        }
    //
    //        int n = in.nextInt();
    //        for (int i = 1; i <=n ; i++) {
    //            set.add(in.nextInt());
    //        }
    //
    //        Object[] result = set.toArray();
    //        Arrays.sort(result);
    //
    //        for(int i=0; i< result.length; i++){
    //            System.out.print(result[i]);
    //        }
    //    }
    }

  

