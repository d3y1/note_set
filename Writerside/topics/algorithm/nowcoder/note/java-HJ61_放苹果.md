# java-HJ61 放苹果


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            while (scanner.hasNext()){
                int m = scanner.nextInt();
                int n = scanner.nextInt();
                System.out.println(count(m, n));
            }
        }
    
        /**
         * 递归
         * @param m
         * @param n
         * @return
         */
        private static int count(int m, int n) {
            if(m == 0 || n == 1) {
                return 1;
            }
            // 当盘子数大于苹果数
            if(n > m) {
                return count(m, n-1);
            } else {
                // 当盘子数<=苹果数
                return count(m, n - 1) + count(m - n, n);
            }
        }
    
       /**
        * 使用动态规划思想求解，记 dp[i][j] 表示使用 i 个苹果放入到 j 个盘子的方案数。
        *
        * 1. 若 i<j，即苹果比盘子数小
        *     (1)比如将 2 个苹果放入 3 个盘子，必然会有一个盘子为空，即{0,x,y}，其中一位固定为 0，不会影响最终的方案数，这和将 2 个苹果放入 2 个盘子的方案数目是一样的，即 {x,y}
        *     (2)因此有当 i<j 时，dp[i][j] = dp[i][i]
        * 2. 若 i>=j，即苹果数目不小于盘子数时，考虑是否允许有空盘子（比如将 4 个苹果放入 3 个盘子）
        *     (1)若允许有空盘，相当于盘子数量少一个（因为固定认为是空盘，不会影响最终方案数目），即 {x,y,0}，这对应着 dp[i][j-1]
        *     (2)若不允许有空盘，对于 j 个盘子，相当于拿出来 j 个苹果，分配到每个盘子中，保证每个盘子分配到一个苹果，这对应着 dp[i−j][j]
        *     (3)因此有当 i>=j 时，dp[i][j] = dp[i][j-1] + dp[i−j][j]
        * 3. 边界条件
        *     (1)对于只有 1 个盘子的情况，分配方案只有 1 种，dp[i][1] = 1;
        *     (2)对于只有 0 个苹果的情况，分配方案只有 1 种，dp[0][j] = 1;
        *     (3)对于只有 1 个苹果的情况，分配方案只有 1 种，dp[1][j] = 1;
        */
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //        while(in.hasNext()){
    //            int apple = in.nextInt();
    //            int dish = in.nextInt();
    //
    //            if(apple == 0 || apple == 1 || dish == 1){
    //                System.out.println(1);
    //                return;
    //            }
    //
    //            int[][] dp = new int[apple+1][dish+1];
    //
    //            // 边界条件
    //            // 1. dp[i][1] = 1;
    //            // 2. dp[0][j] = 1;
    //            // 3. dp[1][j] = 1;   只有一个盘子，分配方案只有1种
    //            for(int i=0;i<=apple;i++){
    //                dp[i][1] = 1;
    //            }
    //            for(int j=0;j<=dish;j++){
    //                dp[0][j] = 1;
    //                dp[1][j] = 1;
    //            }
    //
    //            for(int i=2;i<=apple;i++){
    //                for(int j=2;j<=dish;j++){
    //                    if(i < j){
    //                        //苹果比盘子数小
    //                        //比如将2个苹果放入3个盘子，必然会有一个盘子为空，即 {0,x,y}，即其中一位固定为0，不会影响最终的方案数
    //                        //这和将2个苹果放入2个盘子的方案数目是一样的，即 {x,y}
    //                        dp[i][j] = dp[i][i];
    //                    } else {
    //                        //苹果数目 >= 盘子数, 考虑是否每个盘子都要装苹果
    //                        //比如将4个苹果放入3个盘子，即 {x,y,z} -> dp[i][j]
    //                        //如果不装满所有的盘子，相当于盘子数量少一个，即 {x,y,0} -> dp[i][j-1]
    //                        //如果装满所有的盘子，则所有盘子里面至少有一个苹果，相当于所有盘子里面都去掉一个苹果再进行分配 -> dp[i−j][j]
    //                        dp[i][j] = dp[i][j-1];
    //                        if(i-j >= 0){
    //                            dp[i][j] += dp[i-j][j];
    //                        }
    //                    }
    //                }
    //            }
    //
    //            System.out.println(dp[apple][dish]);
    //        }
    //    }
    }

  

