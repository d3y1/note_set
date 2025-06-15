# java-NC80 把二叉树打印成多行


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
     * NC80 把二叉树打印成多行
     * @author d3y1
     */
    public class Solution {
        private ArrayList<ArrayList<Integer>> lists = new ArrayList<>();
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param pRoot TreeNode类 
         * @return int整型ArrayList<ArrayList<>>
         */
        public ArrayList<ArrayList<Integer>> Print (TreeNode pRoot) {
            levelOrder(pRoot);
            return lists;
        }
    
        /**
         * 层序遍历
         * @param pRoot
         */
        private void levelOrder(TreeNode pRoot){
            if(pRoot == null){
                return;
            }
    
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(pRoot);
    
            int size;
            ArrayList<Integer> list;
            TreeNode node;
            while(!queue.isEmpty()){
                size = queue.size();
                list = new ArrayList<>();
                while(size-- > 0){
                    node = queue.poll();
                    list.add(node.val);
                    if(node.left != null){
                        queue.offer(node.left);
                    }
                    if(node.right != null){
                        queue.offer(node.right);
                    }
                }
                lists.add(list);
            }
        }
    }

  

