# java-NC60 判断二叉树是否为搜索二叉树和完全二叉树


    import java.util.*;
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;
    
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
     * NC60 判断一棵二叉树是否为搜索二叉树和完全二叉树
     * @author d3y1
     */
    public class Solution {
        private boolean[] result = new boolean[]{true, true};
        
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param root TreeNode类 the root
         * @return bool布尔型一维数组
         */
        public boolean[] judgeIt (TreeNode root) {
            return solution1(root);
            // return solution2(root);
        }
    
        private TreeNode pre = null;
        private boolean reachEnd = false;
    
        private boolean[] solution1(TreeNode root){
            inorder(root);
            levelorder(root);
            // levelorder1(root);
            return result;
        }
    
        /**
         * 递归: 中序遍历
         * @param root
         */
        private void inorder(TreeNode root){
            if(root == null){
                return;
            }
    
            inorder(root.left);
    
            if(pre != null){
                if(pre.val > root.val){
                    result[0] = false;
                }
            }
            pre = new TreeNode(root.val);
    
            inorder(root.right);
        }
    
        /**
         * 层序遍历: 队列
         * 完全二叉树在遇到空节点之后剩余的应当全是空节点
         * @param root
         */
        private void levelorder(TreeNode root){
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
            TreeNode node;
            while(queue.peek() != null){
                node = queue.poll();
                queue.offer(node.left);
                queue.offer(node.right);
            }
    
            // 剩余的应当全是空节点
            while(!queue.isEmpty() && queue.peek()==null){
                queue.poll();
            }
    
            if(!queue.isEmpty()){
                result[1] = false;
            }
        }
    
        /**
         * 层序遍历: 队列
         * @param root
         */
        private void levelorder1(TreeNode root){
            if(root == null){
                return;
            }
    
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
            TreeNode node;
            while(!queue.isEmpty()){
                node = queue.poll();
                if(reachEnd){
                    if(node.left!=null || node.right!=null){
                        result[1] = false;
                        break;
                    }
                }else{
                    if(node.left==null && node.right==null){
                        reachEnd = true;
                    }else if(node.left==null && node.right!=null){
                        result[1] = false;
                        break;
                    }else if(node.left!=null && node.right==null){
                        reachEnd = true;
                        queue.offer(node.left);
                    }else{
                        queue.offer(node.left);
                        queue.offer(node.right);
                    }
                }
            }
        }
    
        ////////////////////////////////////////////////////////////////////////////////////////
    
        private LinkedList<Integer> list = new LinkedList<>();
        private StringBuilder sb = new StringBuilder();
    
        private boolean[] solution2(TreeNode root){
            if(root == null){
                return result;
            }
    
            inOrder(root);
            levelOrder(root);
            return result;
        }
    
        /**
         * 中序遍历
         * @param root
         */
        private void inOrder(TreeNode root){
            if(!result[0]){
                return;
            }
            if(root == null){
                return;
            }
    
            inOrder(root.left);
            if(list.size() == 0){
                list.offer(root.val);
            }else{
                if(root.val <= list.getLast()){
                    result[0] = false;
                    return;
                }else{
                    list.offer(root.val);
                }
            }
            inOrder(root.right);
        }
    
        /**
         * 层序遍历
         * @param root
         */
        private void levelOrder(TreeNode root){
            Queue<TreeNode> queue = new LinkedList<>();
            sb.append(root.val);
            queue.offer(root);
    
            TreeNode node;
            while(!queue.isEmpty()){
                node = queue.poll();
                if(node.left != null){
                    sb.append(node.left.val);
                    queue.offer(node.left);
                }else{
                    sb.append("#");
                }
                if(node.right != null){
                    sb.append(node.right.val);
                    queue.offer(node.right);
                }else{
                    sb.append("#");
                }
            }
    
            // #符号后面含有数字
            // String regex = "#[0-9]{1,}";
            String regex = "#\\d+";
            Pattern pattern = Pattern.compile(regex);
            Matcher matcher = pattern.matcher(sb.toString());
            if(matcher.find()){
                result[1] = false;
            }
        }
    }

  

