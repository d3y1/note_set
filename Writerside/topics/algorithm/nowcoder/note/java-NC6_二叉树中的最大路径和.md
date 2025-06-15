# java-NC6 二叉树中的最大路径和


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
     * NC6 二叉树中的最大路径和
     * @author d3y1
     */
    public class Solution {
        private static int sum = Integer.MIN_VALUE;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param root TreeNode类
         * @return int整型
         */
        public int maxPathSum (TreeNode root) {
            postorder(root);
    
            return sum;
        }
    
        /**
         * 后序遍历: 递归
         * @param root
         * @return
         */
        private int postorder(TreeNode root){
            if(root == null){
                return 0;
            }
    
            // 左分支最大路径值
            int leftMaxVal = postorder(root.left);
            // 右分支最大路径值
            int rightMaxVal = postorder(root.right);
            
            // 当前节点处最大路径和: 当前节点值+左分支最大路径值+右分支最大路径值
            // currSum = root.val + max(leftMaxVal,0) + max(rightMaxVal,0)
            int currSum = root.val;
            if(leftMaxVal > 0){
                currSum += leftMaxVal;
            }
            if(rightMaxVal > 0){
                currSum += rightMaxVal;
            }
            sum = Math.max(sum, currSum);
    
            // 当前节点处最大路径值: 当前节点值+(左分支最大路径值|右分支最大路径值) 或者 仅取当前节点值
            // currVal = root.val + max(leftMaxVal,rightMaxVal,0)
            int currVal = root.val;
            int max = Math.max(leftMaxVal, rightMaxVal);
            if(max > 0){
                currVal += max;
            }
    
            return currVal;
        }
    }

  

