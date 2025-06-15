# java-NC223 从中序与后序遍历序列构造二叉树


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
     * NC223 从中序与后序遍历序列构造二叉树
     * @author d3y1
     */
    public class Solution {
        HashMap<Integer,Integer> inMap = new HashMap<>();
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC12 重建二叉树 [nowcoder]
         *
         * @param inorder int整型一维数组 中序遍历序列
         * @param postorder int整型一维数组 后序遍历序列
         * @return TreeNode类
         */
        public TreeNode buildTree (int[] inorder, int[] postorder) {
            // return solution1(inorder, postorder);
            // return solution2(inorder, postorder);
            // return solution22(inorder, postorder);
            return solution3(inorder, postorder);
        }
    
        /**
         * 递归
         * @param inorder
         * @param postorder
         * @return
         */
        private TreeNode solution1(int[] inorder, int[] postorder){
            return construct(inorder, postorder);
        }
    
        /**
         * 递归
         * @param inorder
         * @param postorder
         * @return
         */
        public TreeNode construct(int[] inorder, int[] postorder){
            int n = postorder.length;
            if(n == 0){
                return null;
            }
    
            // 当前根结点
            int rootVal = postorder[n-1];
            TreeNode root = new TreeNode(rootVal);
            // 当前根结点 左子树节点个数
            int left = 0;
            while(inorder[left] != rootVal){
                left++;
            }
            if(left > 0){
                root.left = construct(Arrays.copyOfRange(inorder, 0, left), Arrays.copyOfRange(postorder, 0, left));
            }
            // 当前根结点 右子树节点个数
            int right = n-(left+1);
            if(right > 0){
                root.right = construct(Arrays.copyOfRange(inorder, left+1, n), Arrays.copyOfRange(postorder, left, n-1));
            }
    
            return root;
        }
    
        //////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 哈希 + 递归
         * @param inorder
         * @param postorder
         * @return
         */
        private TreeNode solution2(int[] inorder, int[] postorder){
            int n = inorder.length;
            if(n == 0){
                return null;
            }
    
            // 哈希: val -> idx
            for(int i=0; i<n; i++){
                inMap.put(inorder[i], i);
            }
    
            // 根结点
            TreeNode root = new TreeNode(postorder[n-1]);
            // 递归遍历
            dfs(postorder, root, 0, n-1, 0, n-1);
    
            return root;
        }
    
        /**
         * 递归遍历
         * @param postorder
         * @param root
         * @param inLeft
         * @param inRight
         * @param postLeft
         * @param postRight
         */
        private void dfs(int[] postorder, TreeNode root, int inLeft, int inRight, int postLeft, int postRight){
            int inRootIdx = inMap.get(root.val);
    
            int leftSize = inRootIdx-inLeft;
            int rightSize = inRight-inRootIdx;
    
            // 有左子树
            if(leftSize > 0){
                root.left = new TreeNode(postorder[postLeft+leftSize-1]);
                dfs(postorder, root.left, inLeft, inRootIdx-1, postLeft, postLeft+leftSize-1);
            }
    
            // 有右子树
            if(rightSize > 0){
                root.right = new TreeNode(postorder[postRight-1]);
                dfs(postorder, root.right, inRootIdx+1, inRight, postLeft+leftSize, postRight-1);
            }
        }
    
        //////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 哈希+递归: 简化
         * @param inorder
         * @param postorder
         * @return
         */
        private TreeNode solution22(int[] inorder, int[] postorder){
            int n = inorder.length;
            if(n == 0){
                return null;
            }
    
            // 哈希: val -> idx
            for(int i=0; i<n; i++){
                inMap.put(inorder[i], i);
            }
    
            // 递归遍历
            return dfs(postorder, 0, n-1, 0, n-1);
        }
    
        /**
         * 递归遍历: 简化
         * @param postorder
         * @param inLeft
         * @param inRight
         * @param postLeft
         * @param postRight
         */
        private TreeNode dfs(int[] postorder, int inLeft, int inRight, int postLeft, int postRight){
            TreeNode root = new TreeNode(postorder[postRight]);
            
            int inRootIdx = inMap.get(root.val);
    
            int leftSize = inRootIdx-inLeft;
            int rightSize = inRight-inRootIdx;
    
            // 有左子树
            if(leftSize > 0){
                root.left = dfs(postorder, inLeft, inRootIdx-1, postLeft, postLeft+leftSize-1);
            }
    
            // 有右子树
            if(rightSize > 0){
                root.right = dfs(postorder, inRootIdx+1, inRight, postLeft+leftSize, postRight-1);
            }
    
            return root;
        }
    
        //////////////////////////////////////////////////////////////////////////////////////
    
        // 后序遍历根结点索引
        private int postRootIdx;
    
        private TreeNode solution3(int[] inorder, int[] postorder){
            int n = postorder.length;
            postRootIdx = n-1;
    
            // 哈希: val -> idx
            for(int i=0; i<n; i++){
                inMap.put(inorder[i], i);
            }
    
            return build(postorder, 0, n-1);
        }
    
        /**
         * 递归遍历
         *
         * 二叉树后序遍历: 左 -> 右 -> 根
         * 可利用该性质直接找到后序遍历根节点, 子树遍历先右后左: (根) -> 右 -> 左
         *
         * @param postorder
         * @param inLeft
         * @param inRight
         * @return
         */
        private TreeNode build(int[] postorder, int inLeft, int inRight){
            if(inLeft > inRight){
                return null;
            }
    
            // 根
            int postRootVal = postorder[postRootIdx--];
            TreeNode root = new TreeNode(postRootVal);
    
            if(inLeft == inRight){
                return root;
            }
    
            // 中序遍历根结点索引
            int inRootIdx = inMap.get(postRootVal);
    
            // 右
            root.right = build(postorder, inRootIdx+1, inRight);
            // 左
            root.left = build(postorder, inLeft, inRootIdx-1);
    
            return root;
        }
    }

  

