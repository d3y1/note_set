# java-BD4 蘑菇阵


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
         * 动态规划
         *
         * dp[i][j]表示不碰到蘑菇走到位置(i,j)处的概率
         *
         * 简化
         * dp[i][j] = (j==m?1:0.5) * dp[i-1][j] + (i==n?1:0.5) * dp[i][j-1]
         *
         * @param in
         */
        private static void solution2(Scanner in){
            int n = in.nextInt();
            int m = in.nextInt();
            int k = in.nextInt();
    
            double[][] dp = new double[n+1][m+1];
            boolean[][] mushroom = new boolean[n+1][m+1];
            for(int i=1; i<=k; i++){
                mushroom[in.nextInt()][in.nextInt()] = true;
            }
    
            // 初始化 (1,1)有无蘑菇
            if(mushroom[1][1]){
                dp[1][1] = 0;
            }else{
                dp[1][1] = 1;
            }
    
            for(int i=1; i<=n; i++){
                for(int j=1; j<=m; j++){
                    if(!(i==1 && j==1)){
                        if(mushroom[i][j]){
                            dp[i][j] = 0 * dp[i-1][j] + 0 * dp[i][j-1];
                        }else{
                            dp[i][j] = (j==m?1:0.5) * dp[i-1][j] + (i==n?1:0.5) * dp[i][j-1];
                        }
                    }
                }
            }
    
            System.out.println(String.format("%.2f", dp[n][m]));
        }
    
        /**
         * 动态规划
         *
         * dp[i][j]表示不碰到蘑菇走到位置(i,j)处的概率
         *
         * @param in
         */
        private static void solution1(Scanner in){
            int n = in.nextInt();
            int m = in.nextInt();
            int k = in.nextInt();
    
            double[][] dp = new double[n+1][m+1];
            boolean[][] mushroom = new boolean[n+1][m+1];
            for(int i=1; i<=k; i++){
                mushroom[in.nextInt()][in.nextInt()] = true;
            }
    
            // 起始处(1,1) 有无蘑菇
            if(mushroom[1][1]){
                dp[1][1] = 0;
            }else{
                dp[1][1] = 1;
            }
            // 初始化第一列
            for(int i=2; i<=n; i++){
                if(mushroom[i][1]){
                    dp[i][1] = 0 * dp[i-1][1];
                }else{
                    if(m == 1){
                        dp[i][1] = 1 * dp[i-1][1];
                    }else{
                        dp[i][1] = 0.5 * dp[i-1][1];
                    }
                }
            }
            // 初始化第一行
            for(int i=2; i<=m; i++){
                if(mushroom[1][i]){
                    dp[1][i] = 0 * dp[1][i-1];
                }else{
                    if(n == 1){
                        dp[1][i] = 1 * dp[1][i-1];
                    }else{
                        dp[1][i] = 0.5 * dp[1][i-1];
                    }
                }
            }
    
            for(int i=2; i<=n; i++){
                for(int j=2; j<=m; j++){
                    if(mushroom[i][j]){
                        dp[i][j] = 0 * dp[i-1][j] + 0 * dp[i][j-1];
                    }else{
                        if(i==n && j==m){
                            dp[i][j] = 1 * dp[i-1][j] + 1 * dp[i][j-1];
                        }else if(i == n){
                            dp[i][j] = 0.5 * dp[i-1][j] + 1 * dp[i][j-1];
                        }else if(j == m){
                            dp[i][j] = 1 * dp[i-1][j] + 0.5 * dp[i][j-1];
                        }else{
                            dp[i][j] = 0.5 * dp[i-1][j] + 0.5 * dp[i][j-1];
                        }
                    }
                }
            }
    
            System.out.println(String.format("%.2f", dp[n][m]));
        }
    }

  

