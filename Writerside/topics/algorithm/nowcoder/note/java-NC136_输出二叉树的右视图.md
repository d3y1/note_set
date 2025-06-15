# java-NC136 输出二叉树的右视图


    import java.util.*;
    
    /**
     * NC136 输出二叉树的右视图
     * @author d3y1
     */
    public class Solution {
        private ArrayList<Integer> list = new ArrayList<>();
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 求二叉树的右视图
         * 
         * 相似 -> NC12 重建二叉树 [nowcoder]
         * 相似 -> NC223 从中序与后序遍历序列构造二叉树 [nowcoder]
         * 
         * @param preOrder int整型一维数组 先序遍历
         * @param inOrder int整型一维数组 中序遍历
         * @return int整型一维数组
         */
        public int[] solve (int[] preOrder, int[] inOrder) {
            return solution1(preOrder, inOrder);
            // return solution2(preOrder, inOrder);
        }
    
        // val -> idx
        private HashMap<Integer,Integer> inMap = new HashMap<>();
        private int preRootIdx = 0;
    
        /**
         * 前序遍历 + 层序遍历
         * @param preOrder
         * @param inOrder
         * @return
         */
        private int[] solution1(int[] preOrder, int[] inOrder){
            int n = inOrder.length;
            if(n == 0){
                return new int[]{};
            }
    
            for(int i=0; i<n; i++){
                inMap.put(inOrder[i], i);
            }
    
            // 构建树
            TreeNode root = build(preOrder, 0, n-1);
            // 右视图
            levelOrder(root);
    
            int[] result = new int[list.size()];
            for(int i=0; i<list.size(); i++){
                result[i] = list.get(i);
            }
    
            return result;
        }
    
        /**
         * 递归遍历(前序)
         *
         * 二叉树前序遍历: 根 -> 左 -> 右
         * 可利用该性质直接找到前序遍历根节点, 子树遍历先左后右: (根) -> 左 -> 右
         *
         * @param preOrder
         * @param inLeft
         * @param inRight
         * @return
         */
        private TreeNode build(int[] preOrder, int inLeft, int inRight){
            if(inLeft > inRight){
                return null;
            }
    
            // 根
            int preRootVal = preOrder[preRootIdx++];
            TreeNode root = new TreeNode(preRootVal);
    
            if(inLeft == inRight){
                return root;
            }
    
            // 中序遍历根结点索引
            int inRootIdx = inMap.get(preRootVal);
    
            // 左
            root.left = build(preOrder, inLeft, inRootIdx-1);
            // 右
            root.right = build(preOrder, inRootIdx+1, inRight);
    
    
            return root;
        }
    
        /**
         * 前序遍历 + 层序遍历
         * @param preOrder
         * @param inOrder
         * @return
         */
        private int[] solution2(int[] preOrder, int[] inOrder){
            int n = inOrder.length;
            if(n == 0){
                return new int[]{};
            }
    
            // 构建树
            TreeNode root = construct(preOrder, inOrder);
            // 右视图
            levelOrder(root);
    
            int[] result = new int[list.size()];
            for(int i=0; i<list.size(); i++){
                result[i] = list.get(i);
            }
    
            return result;
        }
    
        /**
         * 递归(前序)
         * @param preOrder
         * @param inOrder
         * @return
         */
        public TreeNode construct(int[] preOrder, int[] inOrder){
            int n = preOrder.length;
            if(n == 0){
                return null;
            }
            // 当前根结点
            int rootVal = preOrder[0];
            TreeNode root = new TreeNode(rootVal);
    
            // 当前根结点 左子树节点个数
            int left = 0;
            while(inOrder[left] != rootVal){
                left++;
            }
            if(left > 0){
                root.left = construct(Arrays.copyOfRange(preOrder, 1, left+1), Arrays.copyOfRange(inOrder, 0, left));
            }
    
            // 当前根结点 右子树节点个数
            int right = n-(left+1);
            if(right > 0){
                root.right = construct(Arrays.copyOfRange(preOrder, left+1, n), Arrays.copyOfRange(inOrder, left+1, n));
            }
    
            return root;
        }
    
        /**
         * 层序遍历
         * @param root
         */
        private void levelOrder(TreeNode root){
            // 双端队列
            Deque<TreeNode> deque = new ArrayDeque<>();
            deque.offerLast(root);
    
            int size;
            TreeNode tNode;
            while(!deque.isEmpty()){
                size = deque.size();
                list.add(deque.peekLast().val);
                while(size-- > 0){
                    tNode = deque.pollFirst();
                    if(tNode.left != null){
                        deque.offerLast(tNode.left);
                    }
                    if(tNode.right != null){
                        deque.offerLast(tNode.right);
                    }
                }
            }
        }
        
        private class TreeNode {
            int val = 0;
            TreeNode left = null;
            TreeNode right = null;
            public TreeNode(int val){
                this.val = val;
            }
        }
    }

  

