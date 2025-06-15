# java-NC215 将二叉搜索树改为累加树


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
     * NC215 将二叉搜索树改为累加树
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param root TreeNode类
         * @return TreeNode类
         */
        public TreeNode convertBST (TreeNode root) {
            // return solution1(root);
            return solution2(root);
            // return solution3(root);
        }
    
        private Integer next;
    
        /**
         * 递归: 中序遍历
         * @param root
         * @return
         */
        private TreeNode solution1(TreeNode root){
            inOrder(root);
            return root;
        }
    
        /**
         * 中序遍历(变体)[右根左]
         * @param root
         */
        private void inOrder(TreeNode root){
            if(root == null){
                return;
            }
    
            // 右根左
            inOrder(root.right);
            // 从后向前 累加
            if(next != null){
                root.val += next;
            }
            next = root.val;
            inOrder(root.left);
        }
    
        ///////////////////////////////////////////////////////////////////////////////////////////
    
        private int sum = 0;
    
        /**
         * 递归: 中序遍历
         * @param root
         * @return
         */
        private TreeNode solution2(TreeNode root){
            inorder(root);
            return root;
        }
    
        /**
         * 中序遍历(变体)[右根左]
         * @param root
         */
        private void inorder(TreeNode root){
            if(root == null){
                return;
            }
    
            // 右根左
            inorder(root.right);
            // 从后向前 累加
            sum += root.val;
            root.val = sum;
            inorder(root.left);
        }
    
        ///////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 迭代: 栈
         * @param root
         * @return
         */
        private TreeNode solution3(TreeNode root){
            operate(root);
            return root;
        }
    
        /**
         * 栈
         * @param root
         */
        private void operate(TreeNode root){
            Stack<TreeNode> stack = new Stack<>();
    
            TreeNode curr;
            while(root!=null || !stack.isEmpty()){
                // 最右边
                while(root != null){
                    stack.push(root);
                    root = root.right;
                }
    
                curr = stack.pop();
                sum += curr.val;
                curr.val = sum;
    
                root = curr.left;
            }
        }
    }

  

