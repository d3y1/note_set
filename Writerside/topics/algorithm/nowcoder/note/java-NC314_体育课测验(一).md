# java-NC314 体育课测验(一)


    import java.util.*;
    
    /**
     * NC314 体育课测验(一)
     * @author d3y1
     */
    public class Solution {
        // 邻接节点
        private HashSet<Integer>[] adj;
        // 入度
        private int[] T;
        private int V;
        private boolean hasCircle = false;
        private int[] flag;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * 转化为 有向图是否有环路
         *
         * @param numProject int整型
         * @param groups int整型ArrayList<ArrayList<>>
         * @return bool布尔型
         */
        public boolean canFinish (int numProject, ArrayList<ArrayList<Integer>> groups) {
            return solution1(numProject, groups);
            // return solution2(numProject, groups);
        }
    
        /**
         * bfs
         * @param numProject
         * @param groups
         * @return
         */
        private boolean solution1(int numProject, ArrayList<ArrayList<Integer>> groups){
            V = numProject;
            adj = new HashSet[V];
            for(int i=0; i<V; i++){
                adj[i] = new HashSet<>();
            }
            T = new int[V];
    
            int u,v;
            for(ArrayList<Integer> group: groups){
                u = group.get(1);
                v = group.get(0);
                // u -> v 可能有自环
                adj[u].add(v);
                T[v]++;
            }
    
            bfs();
    
            return !hasCircle;
        }
    
        /**
         * 层序遍历: 有向图是否有环路
         *
         * 算法:
         * 1 入度为0的顶点加入队列
         * 2 从图中删除该顶点及其相关的边, 更新相关顶点的入度
         * 3 重复步骤1和步骤2, 直到图中所有顶点都被添加到队列中 或者 无法找到入度为0的顶点为止
         * 4 如果图中存在环路, 则无法进行拓扑排序(或者排序得到的数组集合不等于顶点总数), 因为环路意味着存在循环依赖(总会有入度非0的顶点)
         *
         * @return
         */
        private void bfs(){
            Queue<Integer> queue = new LinkedList<>();
            for(int i=0; i<V; i++){
                if(T[i] == 0){
                    queue.offer(i);
                }
            }
    
            int count = 0;
            int u;
            while(!queue.isEmpty()){
                u = queue.poll();
                count++;
                for(Integer v: adj[u]){
                    if(--T[v] == 0){
                        queue.offer(v);
                    }
                }
            }
    
            hasCircle = (count != V);
        }
    
        /**
         * dfs
         * @param numProject
         * @param groups
         * @return
         */
        private boolean solution2(int numProject, ArrayList<ArrayList<Integer>> groups){
            V = numProject;
            adj = new HashSet[V];
            for(int i=0; i<V; i++){
                adj[i] = new HashSet<>();
            }
            flag = new int[V];
    
    
            int u,v;
            for(ArrayList<Integer> group: groups){
                u = group.get(1);
                v = group.get(0);
                // u -> v 可能有自环
                adj[u].add(v);
            }
    
            for(int i=0 ; i<V ; i++){
                if(flag[i] == 0){
                    dfs(i);
                }
            }
    
            return !hasCircle;
        }
    
        /**
         * 递归: 有向图是否有环路
         *
         * 算法:
         * 标记值为0: 代表搜索起点(dfs入口)
         * 标记值为1: 代表搜索中(如果搜索中碰到值标记值为1的节点, 说明有环)
         * 标记值为2: 代表搜索完成(搜索过程无环)
         *
         * @param u
         */
        public void dfs(int u){
            flag[u] = 1;
            for(Integer v: adj[u]){
                if(flag[v] == 0){
                    dfs(v);
                    if(hasCircle){
                        return;
                    }
                }else if(flag[v] == 1){
                    hasCircle = true;
                    return;
                }
            }
            flag[u] = 2;
        }
    }

  

