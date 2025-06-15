# java-MT32 图的闭包


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法
         * @param in
         */
        private static void solution(Scanner in){
            // 点数
            int n = in.nextInt();
            // 边数
            int m = in.nextInt();
    
            boolean[][] hasEdge = new boolean[n+1][n+1];
            int[] degree = new int[n+1];
    
            int u,v;
            for(int i=1; i<=m; i++){
                u = in.nextInt();
                v = in.nextInt();
                degree[u]++;
                degree[v]++;
                if(u < v){
                    hasEdge[u][v] = true;
                }else{
                    hasEdge[v][u] = true;
                }
            }
    
            int result = 0;
            boolean edgeAdded;
            while(true){
                edgeAdded = false;
                for(int i=1; i<=n; i++){
                    for(int j=i+1; j<=n; j++){
                        if(degree[i]+degree[j] >= n){
                            if(!hasEdge[i][j]){
                                result++;
                                degree[i]++;
                                degree[j]++;
                                hasEdge[i][j] = true;
                                edgeAdded = true;
                            }
                        }
                    }
                }
                // 未加新边 退出
                // 已加新边 重新循环
                if(!edgeAdded){
                    break;
                }
            }
            
            System.out.println(result);
        }
    }

  

