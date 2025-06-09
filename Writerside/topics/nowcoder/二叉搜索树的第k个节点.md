# 二叉搜索树的第k个节点
https://www.nowcoder.com/practice/57aa0bab91884a10b5136ca2c087f8ff

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
     * NC81 二叉搜索树的第k个节点
     * @author d3y1
     */
    public class Solution {
        private int result = -1;
        private int seq = 0;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * 中序遍历结果有序
         * 
         * @param proot TreeNode类 
         * @param k int整型 
         * @return int整型
         */
        public int KthNode (TreeNode proot, int k) {
            inorder(proot, k);
    
            return result;
        }
    
        /**
         * 递归: 中序遍历
         * @param proot
         * @param k
         */
        private void inorder(TreeNode proot, int k){
            if(proot==null || seq>=k){
                return;
            }
    
            inorder(proot.left, k);
    
            if(++seq == k){
                result = proot.val;
            }
    
            inorder(proot.right, k);
        }
    }
    

