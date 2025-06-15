# java-HJ41 称砝码


    import java.util.ArrayList;
    import java.util.HashSet;
    import java.util.Scanner;
    
    /**
     * HJ41 称砝码
     * @author d3y1
     */
    public class Main {
        private static int n;
        private static HashSet<Integer> set = new HashSet<>();
    
        public static void main(String[] args) {
            // solution1();
            solution2();
            // solution3();
        }
    
        /**
         * dfs: 超时!
         */
        private static void solution1(){
            Scanner in = new Scanner(System.in);
            // 砝码种类
            n = in.nextInt();
            // 砝码重量
            int[] m = new int[n];
            // 砝码数量
            int[] x = new int[n];
    
            for(int i=0; i<n; i++){
                m[i] = in.nextInt();
            }
    
            for(int i=0; i<n; i++){
                x[i] = in.nextInt();
            }
    
            dfs(m, x, 0, 0);
    
            System.out.println(set.size());
        }
    
        /**
         * dfs
         * @param m
         * @param x
         * @param idx
         * @param sum
         */
        private static void dfs(int[] m, int[] x, int idx, int sum){
            set.add(sum);
    
            if(idx == n){
                return;
            }
    
            // 此处耗时
            for(int i=idx; i<n; i++){
                for(int j=0; j<=x[i]; j++){
                    dfs(m, x, i+1, sum+m[i]*j);
                }
            }
        }
    
        /**
         * 哈希
         */
        private static void solution2(){
            Scanner in = new Scanner(System.in);
            // 砝码种类
            n = in.nextInt();
            // 砝码重量
            int[] m = new int[n];
            // 砝码数量
            int[] x = new int[n];
    
            for(int i=0; i<n; i++){
                m[i] = in.nextInt();
            }
    
            for(int i=0; i<n; i++){
                x[i] = in.nextInt();
            }
    
            set.add(0);
            ArrayList<Integer> weights;
            for(int i=0; i<n; i++){
                weights = new ArrayList<>(set);
                for(int weight: weights){
                    for(int j=1; j<=x[i]; j++){
                        set.add(weight+m[i]*j);
                    }
                }
            }
    
            System.out.println(set.size());
        }
    
        /**
         * 动态规划
         */
        private static void solution3(){
            Scanner in = new Scanner(System.in);
            // 砝码种类
            n = in.nextInt();
            // 砝码重量
            int[] m = new int[n];
            // 砝码数量
            int[] x = new int[n];
    
            for(int i=0; i<n; i++){
                m[i] = in.nextInt();
            }
    
            // 总重量
            int sum = 0;
            for(int i=0; i<n; i++){
                x[i] = in.nextInt();
                sum += m[i]*x[i];
            }
    
            // dp[i]表示砝码能否组成重量i
            boolean[] dp = new boolean[sum+1];
            dp[0] = true;
    
            for(int i=0; i<n; i++){
                for(int j=1; j<=x[i]; j++){
                    // 降序
                    for(int k=sum; k>=m[i]; k--){
                        if(dp[k-m[i]]){
                            dp[k] = true;
                        }
                    }
                }
            }
    
            int kind = 0;
            for(int i=0; i<=sum; i++){
                if(dp[i]){
                    kind++;
                }
            }
    
            System.out.println(kind);
        }
    }

  

