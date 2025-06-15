# java-NC345 城市群数量


    import java.util.*;
    
    /**
     * NC345 城市群数量
     * @author d3y1
     */
    public class Solution {
        private int result = 0;
        private int N;
        private boolean[] isVisited;
        private HashSet<Integer>[] adj;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param m int整型ArrayList<ArrayList<>>
         * @return int整型
         */
        public int citys (ArrayList<ArrayList<Integer>> m) {
            // return solution1(m);
            // return solution2(m);
            return solution3(m);
        }
    
        /**
         * dfs
         * @param m
         * @return
         */
        private int solution1(ArrayList<ArrayList<Integer>> m){
            N = m.size();
            isVisited = new boolean[N];
            adj = new HashSet[N];
            for(int i = 0; i < N; i++){
                adj[i] = new HashSet<>();
            }
    
            for(int i = 0; i < N; i++){
                for(int j = i+1; j < N; j++){
                    if(m.get(i).get(j) == 1){
                        adj[i].add(j);
                        adj[j].add(i);
                    }
                }
            }
    
            for(int i = 0; i < N; i++){
                if(!isVisited[i]){
                    dfs(i);
                    result++;
                }
            }
    
            return result;
        }
    
        /**
         * 递归
         * @param city
         */
        private void dfs(int city){
            if(isVisited[city]){
                return;
            }
    
            isVisited[city] = true;
    
            for(int adjCity: adj[city]){
                dfs(adjCity);
            }
        }
    
        /**
         * bfs
         * @param m
         * @return
         */
        private int solution2(ArrayList<ArrayList<Integer>> m){
            N = m.size();
            isVisited = new boolean[N];
            adj = new HashSet[N];
            for(int i = 0; i < N; i++){
                adj[i] = new HashSet<>();
            }
    
            for(int i = 0; i < N; i++){
                for(int j = i+1; j < N; j++){
                    if(m.get(i).get(j) == 1){
                        adj[i].add(j);
                        adj[j].add(i);
                    }
                }
            }
    
            for(int i = 0; i < N; i++){
                if(!isVisited[i]){
                    bfs(i);
                    result++;
                }
            }
    
            return result;
        }
    
        /**
         * 非递归: 队列
         * @param city
         */
        private void bfs(int city){
            Queue<Integer> queue = new LinkedList<>();
            queue.offer(city);
    
            int currCity;
            while(!queue.isEmpty()){
                currCity = queue.poll();
                isVisited[currCity] = true;
                for(int adjCity: adj[currCity]){
                    if(!isVisited[adjCity]){
                        queue.offer(adjCity);
                    }
                }
            }
        }
    
        /**
         * 并查集
         * @param m
         * @return
         */
        private int solution3(ArrayList<ArrayList<Integer>> m){
            N = m.size();
            if(N == 1){
                return 1;
            }
            UnionFind uf = new UnionFind(N);
    
            for(int i = 0; i < N; i++){
                for(int j = i+1; j < N; j++){
                    if(m.get(i).get(j) == 1){
                        uf.union(i, j);
                    }
                }
            }
    
            return uf.connect();
        }
    
        /**
         * 并查集类
         */
        private class UnionFind{
            // 连通分量
            int connect;
            // 记录父节点
            int[] parent;
    
            // 构造函数 n为结点个数
            UnionFind(int n){
                // 初始连通分量
                this.connect = n;
                this.parent = new int[n];
                for(int i=0; i<n; i++){
                    // 初始父节点指向自己
                    parent[i]=i;
                }
            }
    
            // 找到x的根节点
            int find(int x){
                while(parent[x] != x){
                    x = parent[x];
                }
                return x;
            }
    
            // 连通p和q
            void union(int p, int q){
                int rootP = find(p);
                int rootQ = find(q);
                if(rootP != rootQ){
                    parent[rootP] = rootQ;
                    connect--;
                }
            }
    
            // 返回连通分量
            int connect(){
                return connect;
            }
        }
    }

  

