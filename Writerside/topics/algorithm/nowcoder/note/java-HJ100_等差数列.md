# java-HJ100 等差数列


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * 数学公式
         * @param args
         */
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            int n = in.nextInt();
    
            int result = (n*(4+3*(n-1)))/2;
    
            System.out.print(result);
        }
        
        
    
    //    /**
    //     * 动态规划
    //     * @param args
    //     */
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int n = in.nextInt();
    //
    //        int result = 0;
    //        int[] dp = new int[n+1];
    //        dp[1] = 2;
    //        result = dp[1];
    //
    //        for(int i=2; i<=n; i++){
    //            dp[i] = dp[i-1]+3;
    //            result += dp[i];
    //        }
    //
    //        System.out.print(result);
    //    }
    }

  

