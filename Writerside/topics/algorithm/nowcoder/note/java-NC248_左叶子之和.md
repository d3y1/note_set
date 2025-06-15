# java-NC248 左叶子之和


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
     * NC248 左叶子之和
     * @author d3y1
     */
    public class Solution {
        private int result = 0;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 查询入口
         *
         * @param root TreeNode类
         * @return int整型
         */
        public int sumOfLeftLeaves (TreeNode root) {
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
            }else{
                // 当前节点有左节点 && 左节点为叶子节点
                if(root.left!=null && root.left.left==null && root.left.right==null){
                    result += root.left.val;
                }
            }
    
            preorder(root.left);
            preorder(root.right);
    
            return;
        }
    }

  

