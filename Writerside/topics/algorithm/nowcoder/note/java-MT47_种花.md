# java-MT47 种花


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
         * 贪心
         * @param in
         */
        private static void solution2(Scanner in){
            int n = in.nextInt();
    
            int[] nums = new int[n+1];
            for(int i=1; i<=n; i++){
                nums[i] = in.nextInt();
            }
    
            int result = 0;
            for(int i=1; i+1<=n; i++){
                if(nums[i] > nums[i+1]){
                    result += nums[i]-nums[i+1];
                }
            }
    
            result += nums[n];
    
            System.out.println(result);
        }
    
        /**
         * 动态规划
         * 
         * dp[i]表示前i个花园都完成计划至少需要的天数
         * 
         *         { dp[i-1]                       , nums[i] <= nums[i-1]
         * dp[i] = {
         *         { dp[i-1] + (nums[i]-nums[i-1]) , nums[i] > nums[i-1]
         *
         * @param in
         */
        private static void solution1(Scanner in){
            int n = in.nextInt();
    
            int[] nums = new int[n+1];
            for(int i=1; i<=n; i++){
                nums[i] = in.nextInt();
            }
            
            int[] dp = new int[n+1];
            dp[1] = nums[1];
    
            for(int i=2; i<=n; i++){
                if(nums[i] > nums[i-1]){
                    dp[i] = dp[i-1] + nums[i] - nums[i-1];
                }else{
                    dp[i] = dp[i-1];
                }
            }
    
            System.out.println(dp[n]);
        }
    }

  

