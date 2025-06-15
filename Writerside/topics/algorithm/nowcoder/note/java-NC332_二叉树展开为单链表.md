# java-NC332 二叉树展开为单链表


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
     * NC332 二叉树展开为单链表
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param root TreeNode类
         * @return TreeNode类
         */
        public TreeNode expandTree (TreeNode root) {
            // return solution1(root);
            // return solution2(root);
            // return solution3(root);
            // return solution4(root);
            return solution5(root);
        }
    
        private ArrayList<TreeNode> list = new ArrayList<>();
    
        /**
         * dfs
         * @param root
         * @return
         */
        private TreeNode solution1(TreeNode root){
            preOrderWithList(root);
            rightLinkNodes();
    
            return root;
        }
    
        /**
         * 递归: 前序遍历
         * @param root
         */
        private void preOrderWithList(TreeNode root){
            if(root == null){
                return;
            }
    
            list.add(root);
            preOrderWithList(root.left);
            preOrderWithList(root.right);
        }
    
        /**
         * 右链接各节点
         */
        private void rightLinkNodes(){
            int size = list.size();
            if(size > 0){
                for(int i=1; i<size; i++){
                    list.get(i-1).left = null;
                    list.get(i-1).right = list.get(i);
                }
                list.get(size-1).left = null;
                list.get(size-1).right = null;
            }
        }
    
        /**
         * 非递归: 栈
         * @param root
         * @return
         */
        private TreeNode solution2(TreeNode root){
            Stack<TreeNode> stack = new Stack<>();
    
            if(root == null){
                return null;
            }
    
            stack.push(root);
    
            TreeNode curr;
            TreeNode pre = null;
            while(!stack.isEmpty()){
                curr = stack.pop();
                if(curr.right != null){
                    stack.push(curr.right);
                }
                if(curr.left != null){
                    stack.push(curr.left);
                }
                if(pre != null){
                    pre.left = null;
                    pre.right = curr;
                }
                pre = curr;
            }
            pre.left = null;
            pre.right = null;
    
            return root;
        }
    
        /**
         * 循环遍历(非基本的树遍历)
         * @param root
         * @return
         */
        private TreeNode solution3(TreeNode root){
            if(root == null){
                return null;
            }
    
            TreeNode curr = root;
            TreeNode pre;
            while(curr != null){
                if(curr.left != null){
                    pre = curr.left;
                    while(pre.right != null){
                        pre = pre.right;
                    }
                    pre.right = curr.right;
                    curr.right = curr.left;
                    curr.left = null;
                }
                curr = curr.right;
            }
    
            return root;
        }
    
        ////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 前序遍历
         * @param root
         * @return
         */
        private TreeNode solution4(TreeNode root){
            preOrder(root);
            return root;
        }
    
        // 当前节点的左子树按先序遍历的最右节点
        private TreeNode rightMost;
    
        /**
         * 递归
         * @param root
         */
        public void preOrder(TreeNode root){
            if(root == null){
                return;
            }
    
            rightMost = root;
    
            if(root.left == null){
                preOrder(root.right);
            }else{
                TreeNode right = root.right;
                root.right = root.left;
                preOrder(root.left);
                root.left = null;
                rightMost.right = right;
                preOrder(right);
            }
        }
    
        ////////////////////////////////////////////////////////////////////////////////
    
        // 当前节点的下一节点
        private TreeNode next;
    
        /**
         * 后序遍历(变体)[右左根]
         * 根->左->右 <= 右<-左<-根
         * 
         * @param root
         * @return
         */
        private TreeNode solution5(TreeNode root){
            postOrder(root);
            return root;
        }
    
        /**
         * 递归: 后序遍历(变体)[右左根]
         * 从后往前处理
         * 妙!
         * @param root
         */
        private void postOrder(TreeNode root){
            if(root == null){
                return;
            }
    
            postOrder(root.right);
            postOrder(root.left);
    
            root.left = null;
            root.right = next;
            next = root;
        }
    }

  

