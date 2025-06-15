# java-HJ103 Redraiment的走法


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                // solution1(in);
                solution2(in);
            }
        }
    
    
        /**
         * 动态规划: dp[i]表示到达当前第i个木桩的最多步数
         * @param in
         */
        private static void solution1(Scanner in){
            int num = in.nextInt();
    
            // 木桩
            int[] woods = new int[num+1];
            int[] dp = new int[num+1];
    
            for(int i=1; i<=num; i++){
                woods[i] = in.nextInt();
            }
    
            int result = 0;
            for(int i=1; i<=num; i++){
                for(int j=i-1; j>=0; j--){
                    if(woods[i] > woods[j]){
                        dp[i] = Math.max(dp[i], dp[j]+1);
                    }
                }
                result = Math.max(result, dp[i]);
            }
    
            System.out.println(result);
        }
    
    
        /**
         * 动态规划: dp[i]表示到达当前第i个木桩的最多步数
         *
         * 二分优化: height[steps]表示步数为steps的最低木桩高度height
         */
        private static void solution2(Scanner in){
            int num = in.nextInt();
    
            // 木桩
            int[] woods = new int[num+1];
            // 有序
            int[] height = new int[num+1];
            int[] dp = new int[num+1];
    
            // 初始化
            for(int i=1; i<=num; i++){
                woods[i] = in.nextInt();
            }
            
            int steps = 1;
            height[1] = woods[1];
            dp[1] = 1;
    
            for(int i=2; i<=num; i++){
                if(height[steps] < woods[i]){
                    height[++steps] = woods[i];
                    dp[i] = steps;
                }
                // 寻找第一个大于woods[i]的height[l]
                else{
                    int l = 0;
                    int r = steps;
                    while(l <= r){
                        int mid = (l+r)>>1;
                        if(height[mid] >= woods[i]) {
                            r = mid-1;
                        }else{
                            l = mid+1;
                        }
                    }
                    height[l] = woods[i];
                    dp[i] = l;
                }
            }
    
            System.out.println(steps);
        }
    }

  

