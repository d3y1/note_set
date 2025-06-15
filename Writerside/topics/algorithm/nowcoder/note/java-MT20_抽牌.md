# java-MT20 抽牌


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 动态规划
         *
         * dp[i][j]表示从牌i到牌j甲的得分期望 甲-小明 乙-小方
         *
         *            { nums[i]                          , j-i=0
         * dp[i][j] = { p*nums[i]+(1-p)*nums[j]          , j-i=1
         *            { p*q*(nums[i]+dp[i+2][j]) +
         *              p*(1-q)*(nums[i]+dp[i+1][j-1]) +
         *              (1-p)*q*(nums[j]+dp[i+1][j-1]) +
         *              (1-p)*(1-q)*(nums[j]+dp[i][j-2]) , j-i>1
         *
         * @param in
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
            double p = in.nextInt()/100.0;
            double q = in.nextInt()/100.0;
    
            int[] nums = new int[n];
            for(int i=0; i<n; i++){
                nums[i] = in.nextInt();
            }
    
            double[][] dp = new double[n][n];
            for(int gap=0; gap<n; gap++){
                for(int i=0; i<n; i++){
                    int j = i+gap;
                    if(j < n){
                        if(j == i){
                            dp[i][j] = nums[i];
                        }else if(j == i+1){
                            dp[i][j] = p*nums[i] + (1-p)*nums[j];
                        }else{
                                       //甲上乙上
                            dp[i][j] = p*q*(nums[i] + dp[i+2][j]) +
                                       //甲上乙下
                                       p*(1-q)*(nums[i] + dp[i+1][j-1]) +
                                       //甲下乙上
                                       (1-p)*q*(nums[j] + dp[i+1][j-1]) +
                                       //甲下乙下
                                       (1-p)*(1-q)*(nums[j] + dp[i][j-2]);
                        }
                    }else{
                        break;
                    }
                }
            }
    
            System.out.printf("%.3f", dp[0][n-1]);
        }
    }

  

