# 距离是K的二叉树节点
https://www.nowcoder.com/practice/e280b9b5aabd42c9b36831e522485622

    import java.util.*;
    
    /*
     * public class TreeNode {
     *   int val = 0;
     *   TreeNode left = null;
     *   TreeNode right = null;
     *   public TreeNode(int val) {
     *     this.val = val;
     *   }
     * }
     */
    
    /**
     * NC370 距离是K的二叉树节点
     * @author d3y1
     */
    public class Solution {
        private HashSet<Integer>[] adj;
        private boolean[] isVisited;
        private ArrayList<Integer> result = new ArrayList<>();
        private final int N = 1000;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param root TreeNode类
         * @param target int整型
         * @param k int整型
         * @return int整型一维数组
         */
        public ArrayList<Integer> distanceKnodes (TreeNode root, int target, int k) {
            return solution(root, target, k);
        }
    
        /**
         * dfs + bfs
         * @param root
         * @param target
         * @param k
         * @return
         */
        private ArrayList<Integer> solution(TreeNode root, int target, int k){
            isVisited = new boolean[N];
            adj = new HashSet[N];
            for(int i = 0; i < N; i++){
                adj[i] = new HashSet<>();
            }
    
            postOrder(root);
            levelOrder(target, k);
    
            return result;
        }
    
        /**
         * 递归: 后序遍历
         * @param root
         */
        private void postOrder(TreeNode root){
            if(root == null){
                return;
            }
    
            postOrder(root.left);
            postOrder(root.right);
    
            if(root.left != null){
                adj[root.val].add(root.left.val);
                adj[root.left.val].add(root.val);
            }
            if(root.right != null){
                adj[root.val].add(root.right.val);
                adj[root.right.val].add(root.val);
            }
        }
    
        /**
         * 队列: 层序遍历
         * @param target
         * @param k
         */
        private void levelOrder(int target, int k){
            Queue<Integer> queue = new LinkedList<>();
            isVisited[target] = true;
            queue.offer(target);
    
            int curr;
            int size;
            int level = 0;
            boolean isFound = false;
            while(!queue.isEmpty()){
                level++;
                size = queue.size();
                while(size-- > 0){
                    curr = queue.poll();
                    for(int next: adj[curr]){
                        if(!isVisited[next]){
                            isVisited[next] = true;
                            if(level == k){
                                isFound = true;
                                result.add(next);
                            }else{
                                queue.offer(next);
                            }
                        }
                    }
                }
                if(isFound){
                    break;
                }
            }
        }
    }
    

