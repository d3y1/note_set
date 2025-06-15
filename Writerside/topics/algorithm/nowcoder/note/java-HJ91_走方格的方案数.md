# java-HJ91 走方格的方案数


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * 递归
         * @param args
         */
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                int n = in.nextInt();
                int m = in.nextInt();
    
                System.out.print(dp(m, n));
            }
        }
    
        private static int dp(int m, int n){
            if(m==0 && n==0){
                return 0;
            }else if(m==0 || n==0){
                return 1;
            }else{
                return dp(m, n-1)+dp(m-1, n);
            }
        }
    
    //    private static int dp(int m, int n){
    //        if(m==1 || n==1){
    //            return m+n;
    //        }else{
    //            return dp(m, n-1)+dp(m-1, n);
    //        }
    //    }
        
        
        
    //    /**
    //     * 动态规划
    //     * @param args
    //     */
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        while (in.hasNext()){
    //            int n = in.nextInt();
    //            int m = in.nextInt();
    //
    //            int[][] dp = new int[m+1][n+1];
    //
    //            for(int i=1; i<=m; i++){
    //                dp[i][0] = 1;
    //            }
    //            for(int j=1; j<=n; j++){
    //                dp[0][j] = 1;
    //            }
    //
    //            for(int i=1; i<=m; i++){
    //                for(int j=1; j<=n; j++){
    //                    dp[i][j] = dp[i][j-1] + dp[i-1][j];
    //                }
    //            }
    //
    //            System.out.print(dp[m][n]);
    //        }
    //    }
    }

  

