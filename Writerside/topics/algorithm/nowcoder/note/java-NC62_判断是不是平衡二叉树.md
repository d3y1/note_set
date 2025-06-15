# java-NC62 判断是不是平衡二叉树


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
     * NC62 判断是不是平衡二叉树
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序人口
         *
         * @param pRoot TreeNode类
         * @return bool布尔型
         */
        public boolean IsBalanced_Solution (TreeNode pRoot) {
            return solution1(pRoot);
            // return solution2(pRoot);
        }
    
        /**
         * 自底向上
         * @param pRoot
         * @return
         */
        private boolean solution1(TreeNode pRoot){
            int result = dep(pRoot);
            if(result == -1){
                return false;
            }
    
            return true;
        }
    
        /**
         * dfs: 递归(后序遍历)
         * @param pRoot
         * @return
         */
        private int dep(TreeNode pRoot){
            if(pRoot == null){
                return 0;
            }
            int lDep = dep(pRoot.left);
            if(lDep == -1){
                return -1;
            }
            int rDep = dep(pRoot.right);
            if(rDep == -1){
                return -1;
            }
            int gap = Math.abs(lDep-rDep);
            if(gap > 1){
                return -1;
            }
    
            return Math.max(lDep, rDep)+1;
        }
    
        /**
         * 自顶向下
         * @param pRoot
         * @return
         */
        private boolean solution2(TreeNode pRoot){
            return isBalanced(pRoot);
        }
    
        /**
         * dfs
         * @param pRoot
         * @return
         */
        private boolean isBalanced(TreeNode pRoot){
            if(pRoot == null){
                return true;
            }
            if(Math.abs(depth(pRoot.left)-depth(pRoot.right)) > 1){
                return false;
            }
    
            return isBalanced(pRoot.left)&&isBalanced(pRoot.right);
        }
    
        /**
         * 递归
         * @param pRoot
         * @return
         */
        private int depth(TreeNode pRoot){
            if(pRoot == null){
                return 0;
            }
    
            return Math.max(depth(pRoot.left), depth(pRoot.right))+1;
        }
    }

  

