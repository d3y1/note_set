# java-NC195 二叉树的直径


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
     * NC195 二叉树的直径
     * @author d3y1
     */
    public class Solution {
        private int result = 0;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param root TreeNode类 
         * @return int整型
         */
        public int diameterOfBinaryTree (TreeNode root) {
            return solution1(root);
        }
    
        /**
         * dfs
         * @param root
         * @return
         */
        private int solution1(TreeNode root){
            dep(root);
            return result;
        }
    
        /**
         * 递归(后序遍历)
         * @param root
         * @return
         */
        private int dep(TreeNode root){
            if(root == null){
                return 0;
            }
            int lDep = dep(root.left);
            int rDep = dep(root.right);
    
            result = Math.max(result, lDep+rDep);
    
            return Math.max(lDep, rDep)+1;
        }
    }

  

