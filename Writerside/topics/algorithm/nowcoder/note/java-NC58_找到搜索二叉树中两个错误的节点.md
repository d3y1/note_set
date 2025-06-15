# java-NC58 找到搜索二叉树中两个错误的节点


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
     * NC58 找到搜索二叉树中两个错误的节点
     * @author d3y1
     */
    public class Solution {
        private int[] result = new int[2];
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param root TreeNode类 the root
         * @return int整型一维数组
         */
        public int[] findError (TreeNode root) {
            // return solution1(root);
            return solution2(root);
        }
    
        private int seq = 1;
    
        private int[] solution1(TreeNode root){
            inorder(root);
            return result;
        }
    
        /**
         * 中序遍历
         * @param root
         */
        private void inorder(TreeNode root){
            if(root == null){
                return;
            }
    
            inorder(root.left);
    
            if(root.val != seq){
                result[0] = root.val;
                result[1] = seq;
            }
            seq++;
    
            inorder(root.right);
        }
    
        /////////////////////////////////////////////////////////////////////////////////////////
    
        private int idx = 1;
        private int val = 1;
        
        private int[] solution2(TreeNode root){
            inOrder(root);
            return result;
        }
    
        /**
         * 中序遍历
         * @param root
         */
        private void inOrder(TreeNode root){
            if(root == null){
                return;
            }
    
            inOrder(root.left);
            if(root.val != (val++)){
                result[idx--] = root.val;
            }
            inOrder(root.right);
        }
    }

  

