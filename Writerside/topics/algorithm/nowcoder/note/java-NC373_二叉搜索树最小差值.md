# java-NC373 二叉搜索树最小差值


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
     * NC373 二叉搜索树最小差值
     * @author d3y1
     */
    public class Solution {
        private int result = Integer.MAX_VALUE;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param root TreeNode类
         * @return int整型
         */
        public int minDifference (TreeNode root) {
            preorder(root);
    
            return result;
        }
    
        /**
         * 递归: 前序遍历
         * @param root
         */
        private void preorder(TreeNode root){
            if(root == null){
                return;
            }
            if(root.left != null){
                result = Math.min(result, Math.abs(root.val-root.left.val));
            }
            if(root.right != null){
                result = Math.min(result, Math.abs(root.val-root.right.val));
            }
    
            preorder(root.left);
            preorder(root.right);
        }
    }

  

