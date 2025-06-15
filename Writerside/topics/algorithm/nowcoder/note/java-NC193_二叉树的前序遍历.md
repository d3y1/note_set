# java-NC193 二叉树的前序遍历


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
     * NC193 二叉树的前序遍历
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序人口
         *
         * @param root TreeNode类
         * @return int整型一维数组
         */
        public int[] preorderTraversal (TreeNode root) {
            return solution1(root);
            // return solution2(root);
        }
    
        /**
         * dfs
         * @param root
         * @return
         */
        private int[] solution1(TreeNode root){
            List<Integer> list = new ArrayList<>();
    
            preorder(list, root);
    
            int[] result = new int[list.size()];
            for(int i=0; i<list.size(); i++){
                result[i] = list.get(i);
            }
    
            return result;
        }
    
        /**
         * 递归
         * @param list
         * @param root
         */
        private void preorder(List<Integer> list, TreeNode root){
            // 空节点
            if(root == null){
                return;
            }
    
            // 根节点
            list.add(root.val);
            // 左子树
            preorder(list, root.left);
            // 右子树
            preorder(list, root.right);
        }
    
        /**
         * 非递归: 栈
         * @param root
         * @return
         */
        private int[] solution2(TreeNode root){
            List<Integer> list = new ArrayList<>();
            Stack<TreeNode> stack = new Stack<>();
    
            if(root == null){
                return new int[0];
            }
    
            stack.push(root);
    
            TreeNode node;
            while(!stack.isEmpty()){
                node = stack.pop();
                list.add(node.val);
                if(node.right != null){
                    stack.push(node.right);
                }
                if(node.left != null){
                    stack.push(node.left);
                }
            }
    
            int[] result = new int[list.size()];
            for(int i=0; i<list.size(); i++){
                result[i] = list.get(i);
            }
            
            return result;
        }
    }

  

