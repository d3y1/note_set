# java-MT17 共享单车


    import java.util.Comparator;
    import java.util.HashSet;
    import java.util.PriorityQueue;
    import java.util.Scanner;
    
    public class Main {
        // 当前节点的邻接边
        private static HashSet<Edge>[] adj;
        // 当前节点是否有车
        private static int[] hasBike;
        // 骑车或走路情况下 从起点1到达当前节点所需的最少时间
        private static long[][] cost;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法: dijkstra
         * @param in
         */
        private static void solution(Scanner in){
            // 点数
            int V = in.nextInt();
            // 边数
            int E = in.nextInt();
    
            // 构建图 点的范围[1:V]
            adj = new HashSet[V+1];
            for(int i=1; i<=V; i++){
                adj[i] = new HashSet<>();
            }
            int u,v,w;
            for(int i=1; i<=E; i++){
                u = in.nextInt();
                v = in.nextInt();
                w = in.nextInt();
                adj[u].add(new Edge(v, w));
                adj[v].add(new Edge(u, w));
            }
    
            int k = in.nextInt();
            hasBike = new int[V+1];
            for(int i=1; i<=k; i++){
                hasBike[in.nextInt()] = 1;
            }
    
            // init
            cost = new long[2][V+1];
            for(int i=0; i<=1; i++){
                for(int j=1; j<=V; j++){
                    cost[i][j] = Long.MAX_VALUE;
                }
            }
    
            System.out.println(dijkstra(V));
        }
    
        /**
         * dijkstra
         * @param terminal
         * @return
         */
        private static long dijkstra(int terminal){
            // 最小堆(到达当前节点所需的时间)
            PriorityQueue<Node> queue = new PriorityQueue<>();
    
            // init
            queue.offer(new Node(1, 0, hasBike[1]));
            cost[hasBike[1]][1] = 0;
    
            while(!queue.isEmpty()){
                Node curr = queue.poll();
                if(curr.vertex == terminal){
                    return curr.cost;
                }
    
                long time;
                int biked;
                for(Edge e: adj[curr.vertex]){
                    // 骑车
                    if(curr.biked == 1){
                        time = curr.cost + e.weight/2;
                    }
                    // 走路
                    else{
                        time = curr.cost + e.weight;
                    }
    
                    // 能骑则骑
                    biked = (curr.biked | hasBike[e.vertex]);
    
                    if(time < cost[biked][e.vertex]){
                        cost[biked][e.vertex] = time;
                        queue.offer(new Node(e.vertex, time, biked));
                    }
                }
            }
    
            return -1;
        }
    
        private static class Edge{
            int vertex;
            int weight;
    
            public Edge(int vertex, int weight){
                this.vertex = vertex;
                this.weight = weight;
            }
        }
    
        private static class Node implements Comparable<Node>{
            // 当前节点编号
            int vertex;
            // 从起点1到达当前节点所需的最少时间
            long cost;
            // 是否骑车
            int biked;
    
            public Node(int vertex, long cost, int biked){
                this.vertex = vertex;
                this.cost = cost;
                this.biked = biked;
            }
    
            @Override
            public int compareTo(Node o){
                return (int) (this.cost-o.cost);
            }
        }
    }

  

