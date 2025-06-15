# java-MT22 双袋购物


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
                solution3(in);
            }
        }
    
        /**
         * 动态规划: 01背包(一维)[正+反]
         * 
         * dp[j]表示体积不超过j的最大价值
         * 
         * dpA[j] = Math.max(dpA[j], dpA[j-volumes[i]]+values[i])
         * 
         * dpB[j] = Math.max(dpB[j], dpB[j-volumes[i]]+values[i])
         * 
         * @param in
         */
        private static void solution1(Scanner in){
            int n = in.nextInt();
            int bagA = in.nextInt();
            int bagB = in.nextInt();
    
            int[] volumes = new int[n+1];
            int[] values = new int[n+1];
            for(int i=1; i<=n; i++){
                volumes[i] = in.nextInt();
                values[i] = in.nextInt();
            }
    
            int result = 0;
    
            // 正
            int[] dpA = new int[bagA+1];
            int[] ansA = new int[n+2];
            for(int i=1; i<n; i++){
                for(int j=bagA; j>=0; j--){
                    // 选择装袋
                    if(j >= volumes[i]){
                        dpA[j] = Math.max(dpA[j], dpA[j-volumes[i]]+values[i]);
                    }
                }
                ansA[i] = dpA[bagA];
            }
    
            // 反
            int[] dpB = new int[bagB+1];
            int[] ansB = new int[n+2];
            for(int i=n; i>0; i--){
                for(int j=bagB; j>=0; j--){
                    // 选择装袋
                    if(j >= volumes[i]){
                        dpB[j] = Math.max(dpB[j], dpB[j-volumes[i]]+values[i]);
                    }
                }
                ansB[i] = dpB[bagB];
            }
    
            // i点 换袋子
            for(int i=0; i<=n; i++){
                result = Math.max(result, ansA[i]+ansB[i+1]);
            }
    
            System.out.println(result);
        }
    
        /**
         * 动态规划: 01背包(二维)[正+反]
         *
         * dp[i][j]表示前i个物品体积不超过j的最大价值
         *
         * dpA[i][j] = dpA[i-1][j]
         * dpA[i][j] = Math.max(dpA[i][j], dpA[i-1][j-volumes[i]]+values[i])
         *
         * dpB[i][j] = dpB[i+1][j]
         * dpB[i][j] = Math.max(dpB[i][j], dpB[i+1][j-volumes[i]]+values[i])
         *
         * @param in
         */
        private static void solution2(Scanner in){
            int n = in.nextInt();
            int bagA = in.nextInt();
            int bagB = in.nextInt();
    
            int[] volumes = new int[n+1];
            int[] values = new int[n+1];
            for(int i=1; i<=n; i++){
                volumes[i] = in.nextInt();
                values[i] = in.nextInt();
            }
    
            int result = 0;
    
            // 正
            int[][] dpA = new int[n+2][bagA+1];
            for(int i=1; i<n; i++){
                for(int j=bagA; j>=0; j--){
                    // 直接跳过
                    dpA[i][j] = dpA[i-1][j];
    
                    // 选择装袋
                    if(j >= volumes[i]){
                        dpA[i][j] = Math.max(dpA[i][j], dpA[i-1][j-volumes[i]]+values[i]);
                    }
                }
            }
    
            // 反
            int[][] dpB = new int[n+2][bagB+1];
            for(int i=n; i>0; i--){
                for(int j=bagB; j>=0; j--){
                    // 直接跳过
                    dpB[i][j] = dpB[i+1][j];
    
                    // 选择装袋
                    if(j >= volumes[i]){
                        dpB[i][j] = Math.max(dpB[i][j], dpB[i+1][j-volumes[i]]+values[i]);
                    }
                }
            }
    
            // i点 换袋子
            for(int i=0; i<=n; i++){
                result = Math.max(result, dpA[i][bagA]+dpB[i+1][bagB]);
            }
    
            System.out.println(result);
        }
    
        /**
         * 动态规划: 01背包(二维) 超时!
         *
         * dp[i][j]表示前i个物品体积不超过j的最大价值
         *
         * dpA[i][j] = dpA[i-1][j]
         * dpA[i][j] = Math.max(dpA[i][j], dpA[i-1][j-volumes[i]]+values[i])
         *
         * dpB[i][j] = dpB[i-1][j]
         * dpB[i][j] = Math.max(dpB[i][j], dpB[i-1][j-volumes[i]]+values[i])
         *
         * @param in
         */
        private static void solution3(Scanner in){
            int n = in.nextInt();
            int bagA = in.nextInt();
            int bagB = in.nextInt();
    
            int[] volumes = new int[n+1];
            int[] values = new int[n+1];
            for(int i=1; i<=n; i++){
                volumes[i] = in.nextInt();
                values[i] = in.nextInt();
            }
    
            int result = 0;
            // 过point点后 换袋子
            for(int point=0; point<=n; point++){
                int[][] dpA = new int[n+1][bagA+1];
                int[][] dpB = new int[n+1][bagB+1];
                for(int i=1; i<=n; i++){
                    if(i <= point){
                        for(int j=bagA; j>=0; j--){
                            // 直接跳过
                            dpA[i][j] = dpA[i-1][j];
    
                            // 选择装袋
                            if(j >= volumes[i]){
                                dpA[i][j] = Math.max(dpA[i][j], dpA[i-1][j-volumes[i]]+values[i]);
                            }
                        }
                    }else{
                        for(int j=bagB; j>=0; j--){
                            // 直接跳过
                            dpB[i][j] = dpB[i-1][j];
    
                            // 选择装袋
                            if(j >= volumes[i]){
                                dpB[i][j] = Math.max(dpB[i][j], dpB[i-1][j-volumes[i]]+values[i]);
                            }
                        }
                    }
                }
                result = Math.max(result, dpA[point][bagA]+dpB[n][bagB]);
            }
    
            System.out.println(result);
        }
    }

  

