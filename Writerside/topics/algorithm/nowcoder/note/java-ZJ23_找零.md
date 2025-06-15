# java-ZJ23 找零


    import java.util.Scanner;
    
    public class Main {
        private static final int[] coins = new int[]{64, 16, 4, 1};
        private static final int OWN = 1024;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
            }
        }
    
        /**
         * 模拟法: 贪心
         */
        private static void solution1(Scanner in){
            int pay = in.nextInt();
            int money = OWN-pay;
    
            int result = 0;
            int len = coins.length;
            for(int i=0; i<len; i++){
                result += money/coins[i];
                money %= coins[i];
            }
    
            System.out.println(result);
        }
    
        /**
         * 动态规划
         *
         * dp[i]表示找零为i时收到的最少硬币数
         * 
         * dp[i] = Math.min(dp[i], dp[i-coins[j]]+1)
         * 
         * @param in
         */
        private static void solution2(Scanner in){
            int pay = in.nextInt();
            int money = OWN-pay;
    
            int[] dp = new int[money+1];
            int len = coins.length;
            for(int i=1; i<=money; i++){
                dp[i] = i;
                for(int j=0; j<len; j++){
                    if(i >= coins[j]){
                        dp[i] = Math.min(dp[i], dp[i-coins[j]]+1);
                    }
                }
            }
    
            System.out.println(dp[money]);
        }
    }

  

