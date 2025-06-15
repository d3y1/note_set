# java-ZJ22 毕业旅行问题


    import java.util.*;
    public class Main {
        private static int N;
        private static int[][] price;
    
        private static boolean[] visited;
        private static int result = Integer.MAX_VALUE;
    
        public static int[][] dp;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                // solution2(in);
            }
        }
        
        /**
         * 动态规划: 状态压缩
         *
         * dp[i][V]: 代表从i城市出发, 经过V中所有节点, 再回到北京的最低费用.
         * dp[i][V] = min(Price(i,k) + dp[k][V']) for k in V, V'=V-k
         * 
         * @param in
         */
        private static void solution1(Scanner in){
            N = in.nextInt();
            price = new int[N+1][N+1];
            for(int i=0; i<N; i++){
                for(int j=0; j<N; j++){
                    price[i][j] = in.nextInt();
                }
            }
    
            // 对1进行左移n-1位 值等于2^(N-1)
            int V = 1 << (N-1);
            dp = new int[N][V];
            // 初始化
            for (int i=0; i<N; i++) {
                for(int j=0; j<V; j++) {
                    dp[i][j] = -1;
                }
            }
            // 2^3 - 1 = 7 -> (二进制111) -> 节点321
            // 从0城市(北京)出发, 经过V中所有节点(城市123), 再回到北京的最低费用.
            int ans = travel1(0 , V-1);
            System.out.println(ans);
        }
    
        /**
         * DFS
         * @param curr
         * @param cities
         * @return
         */
        public static int travel1(int curr, int cities) {
            if(cities == 0){
                return price[curr][0];
            }
    
            // 命中返回
            if(dp[curr][cities] != -1){
                return dp[curr][cities];
            }
    
            int ans = Integer.MAX_VALUE;
            for(int k=1; k<N; k++){
                // i节点在V中
                if(((cities>>(k-1)) & 1) == 1){
                    // 异或 去掉i节点
                    cities ^= (1<<(k-1));
                    // 记录该轮的最小答案
                    ans = Math.min(ans, price[curr][k]+travel1(k, cities));
                    // 异或 恢复i节点
                    cities ^= (1<<(k-1));
                }
            }
    
            dp[curr][cities] = ans;
            return ans;
        }
    
    
        /**
         * DFS: 超时
         * @param in
         */
        private static void solution2(Scanner in){
            N = in.nextInt();
            visited = new boolean[N+1];
            price = new int[N+1][N+1];
            for(int i=1; i<=N; i++){
                for(int j=1; j<=N; j++){
                    price[i][j] = in.nextInt();
                }
            }
    
            travel2(0, 0, 1);
    
            System.out.println(result);
        }
    
        private static void travel2(int cities, int total, int curr){
            if(cities==N && curr==1){
                result = Math.min(result, total);
            }
    
            for(int i=1; i<=N; i++){
                if(i!=curr && !visited[i]){
                    visited[i] = true;
    
                    travel2(cities+1, total+price[curr][i], i);
    
                    visited[i] = false;
                }
            }
        }
    }

  

