# java-NC234 二叉树的最小深度


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
     * NC234 二叉树的最小深度
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param root TreeNode类 
         * @return int整型
         */
        public int run (TreeNode root) {
            // return solution1(root);
            return solution11(root);
            // return solution2(root);
        }
    
        /**
         * 递归: 后序遍历
         * @param root
         * @return
         */
        private int solution1(TreeNode root){
            return postOrder(root);
        }
    
        /**
         * 后序遍历
         * @param root
         * @return
         */
        private int postOrder(TreeNode root){
            if(root == null){
                return 0;
            }
    
            int leftDep = postOrder(root.left);
            int rightDep = postOrder(root.right);
    
            int curDep;
            if(leftDep>0 && rightDep>0){
                curDep = Math.min(leftDep, rightDep)+1;
            }else if(leftDep>0 && rightDep==0){
                curDep = leftDep+1;
            }else if(leftDep==0 && rightDep>0){
                curDep = rightDep+1;
            }else{
                curDep = 1;
            }
    
            return curDep;
        }
    
        private int result = Integer.MAX_VALUE;
    
        /**
         * 递归: 后序遍历
         * @param root
         * @return
         */
        private int solution11(TreeNode root){
            if(root == null){
                return 0;
            }
    
            postorder(root, 1);
    
            return result;
        }
    
        /**
         * 后序遍历
         * @param root
         * @param depth
         */
        private void postorder(TreeNode root, int depth){
            if(root == null){
                return;
            }
    
            if(depth < result){
                postorder(root.left, depth+1);
                postorder(root.right, depth+1);
                // 当前节点 叶子节点
                if(root.left==null && root.right==null){
                    result = depth;
                }
            }
        }
    
        /**
         * 迭代: 层序遍历
         * @param root
         * @return
         */
        private int solution2(TreeNode root){
            return levelOrder(root);
        }
    
        /**
         * 层序遍历
         * @param root
         * @return
         */
        private int levelOrder(TreeNode root){
            if(root == null){
                return 0;
            }
    
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
    
            int dep = 0;
            int size;
            TreeNode node;
            while(!queue.isEmpty()){
                size = queue.size();
                dep++;
                while(size-- > 0){
                    node = queue.poll();
                    // 第一个 叶子节点
                    if(node.left==null && node.right==null){
                        return dep;
                    }else{
                        if(node.left != null){
                            queue.offer(node.left);
                        }
                        if(node.right != null){
                            queue.offer(node.right);
                        }
                    }
                }
            }
    
            return dep;
        }
    }

  

