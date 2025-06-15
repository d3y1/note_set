# java-NC198 判断是不是完全二叉树


    import java.util.*;
    
    /*
     * public class TreeNode {
     *   int val = 0;
     *   TreeNode left = null;
     *   TreeNode right = null;
     *   public TreeNode(int val) {
     *     this.val = val;
     *   }
     * }
     */
    
    /**
     * NC198 判断是不是完全二叉树
     * @author d3y1
     */
    public class Solution {
        private int seq = 0;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param root TreeNode类
         * @return bool布尔型
         */
        public boolean isCompleteTree (TreeNode root) {
            return solution1(root);
            // return solution2(root);
        }
    
        /**
         * dfs
         * 
         * 最后判断 节点个数与节点序号是否相等
         * 
         * @param root
         * @return
         */
        private boolean solution1(TreeNode root){
            // count-节点个数 seq-节点序号
            int count = postOrder(root, 1);
    
            return count==seq;
        }
    
        /**
         * 递归: 后序遍历
         * 
         * 完全二叉树
         * 如果当前节点索引是idx(索引从1开始), 那么他的左右子节点索引为:
         * left = 2*idx
         * right = 2*idx+1
         * 
         * @param root
         * @param idx
         * @return
         */
        private int postOrder(TreeNode root, int idx){
            if(root == null){
                return 0;
            }
    
            seq = Math.max(seq, idx);
    
            int leftCount = postOrder(root.left, 2*idx);
            int rightCount = postOrder(root.right, 2*idx+1);
    
            return leftCount+rightCount+1;
        }
    
        /**
         * bfs
         * @param root
         * @return
         */
        private boolean solution2(TreeNode root){
            return levelOrder(root);
        }
    
        /**
         * 层序遍历: 队列
         * 完全二叉树在遇到空节点之后剩余的应当全是空节点
         * @param root
         * @return
         */
        private boolean levelOrder(TreeNode root){
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
    
            TreeNode node;
            while(queue.peek() != null){
                node = queue.poll();
                queue.offer(node.left);
                queue.offer(node.right);
            }
    
            // 剩余的应当全是空节点
            while(!queue.isEmpty() && queue.peek()==null){
                queue.poll();
            }
    
            return queue.isEmpty();
        }
    }

  

