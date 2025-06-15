# java-MT23 友好城市


    import java.util.Scanner;
    
    public class Main {
        private static int n;
        private static int k;
        private static int[][] dist;
        private static int[] cities;
        private static int result = Integer.MAX_VALUE;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 图: 邻接矩阵
         * @param in
         */
        private static void solution(Scanner in){
            n = in.nextInt();
    
            dist = new int[n+1][n+1];
            for(int i=1; i<=n; i++){
                for(int j=1; j<=n; j++){
                    dist[i][j] = in.nextInt();
                }
            }
    
            k = in.nextInt();
            cities = new int[2*k];
            for(int i=0; i<2*k; i++){
                cities[i] = in.nextInt();
            }
    
            floyd();
            dfs(0, 0);
    
            System.out.println(result);
        }
    
        /**
         * floyd算法: 多源最短路(多对多)算法
         */
        private static void floyd(){
            for(int k=1; k<=n; k++){
                for(int i=1; i<=n; i++){
                    for(int j=1; j<=n; j++){
                        if(i!=j && dist[i][k]!=-1 && dist[k][j]!=-1){
                            if(dist[i][j] == -1){
                                dist[i][j] = dist[i][k] + dist[k][j];
                            }else{
                                dist[i][j] = Math.min(dist[i][j], dist[i][k]+dist[k][j]);
                            }
                        }
                    }
                }
            }
        }
    
        /**
         * 递归遍历
         * @param cnt
         * @param total
         */
        private static void dfs(int cnt, int total){
            if(cnt == 2*k){
                result = Math.min(result, total);
                return;
            }
    
            for(int i=cnt+1; i<2*k; i++){
                swap(i, cnt+1);
                dfs(cnt+2, total+dist[cities[cnt]][cities[cnt+1]]);
                swap(i, cnt+1);
            }
        }
    
        /**
         * 交换
         * @param i
         * @param j
         */
        private static void swap(int i, int j){
            int tmp = cities[i];
            cities[i] = cities[j];
            cities[j] = tmp;
        }
    }

  

