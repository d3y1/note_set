# java-NC370 距离是K的二叉树节点


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
     * NC370 距离是K的二叉树节点
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param root TreeNode类
         * @param target int整型
         * @param k int整型
         * @return int整型一维数组
         */
        public ArrayList<Integer> distanceKnodes (TreeNode root, int target, int k) {
            // return solution1(root, target, k);
            return solution2(root, target, k);
        }
    
        private HashSet<Integer>[] adj;
        private boolean[] isVisited;
        private ArrayList<Integer> result = new ArrayList<>();
        private final int N = 1000;
    
        /**
         * 后序遍历 + 层序遍历
         * 
         * 图模型
         * 
         * @param root
         * @param target
         * @param k
         * @return
         */
        private ArrayList<Integer> solution1(TreeNode root, int target, int k){
            isVisited = new boolean[N];
            adj = new HashSet[N];
            for(int i = 0; i < N; i++){
                adj[i] = new HashSet<>();
            }
    
            postOrder(root);
            levelOrder(target, k);
    
            return result;
        }
    
        /**
         * 递归: 后序遍历
         * @param root
         */
        private void postOrder(TreeNode root){
            if(root == null){
                return;
            }
    
            postOrder(root.left);
            postOrder(root.right);
    
            if(root.left != null){
                adj[root.val].add(root.left.val);
                adj[root.left.val].add(root.val);
            }
            if(root.right != null){
                adj[root.val].add(root.right.val);
                adj[root.right.val].add(root.val);
            }
        }
    
        /**
         * 队列: 层序遍历
         * @param target
         * @param k
         */
        private void levelOrder(int target, int k){
            Queue<Integer> queue = new LinkedList<>();
            isVisited[target] = true;
            queue.offer(target);
    
            int curr;
            int size;
            int level = 0;
            boolean isFound = false;
            while(!queue.isEmpty()){
                level++;
                size = queue.size();
                while(size-- > 0){
                    curr = queue.poll();
                    for(int next: adj[curr]){
                        if(!isVisited[next]){
                            isVisited[next] = true;
                            if(level == k){
                                isFound = true;
                                result.add(next);
                            }else{
                                queue.offer(next);
                            }
                        }
                    }
                }
                if(isFound){
                    break;
                }
            }
        }
    
        //////////////////////////////////////////////////////////////////////////////////////////
    
        private ArrayList<Integer> list = new ArrayList<>();
        private HashMap<Integer,TreeNode> parentMap = new HashMap<>();
    
        /**
         * 层序遍历 + 前序遍历
         * @param root
         * @param target
         * @param k
         * @return
         */
        private ArrayList<Integer> solution2(TreeNode root, int target, int k){
            if(root == null){
                return list;
            }
    
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
            parentMap.put(root.val, null);
    
    
            TreeNode node,cNode,pNode;
            while(!queue.isEmpty()){
                node = queue.poll();
                if(node.val == target){
                    if(k == 0){
                        list.add(node.val);
                        return list;
                    }
                    downKnodes(node, k);
                    cNode = node;
                    pNode = parentMap.get(cNode.val);
                    while(pNode!=null && k>0){
                        upKnodes(cNode, pNode, --k);
                        cNode = pNode;
                        pNode = parentMap.get(cNode.val);
                    }
    
                    return list;
                }
                if(node.left != null){
                    parentMap.put(node.left.val, node);
                    queue.offer(node.left);
                }
                if(node.right != null){
                    parentMap.put(node.right.val, node);
                    queue.offer(node.right);
                }
            }
    
            return list;
        }
    
        /**
         * 向上遍历
         * @param cNode
         * @param pNode
         * @param k
         */
        private void upKnodes(TreeNode cNode, TreeNode pNode, int k){
            if(k == 0){
                list.add(pNode.val);
                return;
            }
    
            if(pNode.left!=null && pNode.left.val!=cNode.val){
                downKnodes(pNode.left, k-1);
            }
    
            if(pNode.right!=null && pNode.right.val!=cNode.val){
                downKnodes(pNode.right, k-1);
            }
        }
    
        /**
         * 向下遍历
         * @param root
         * @param k
         */
        private void downKnodes(TreeNode root, int k){
            preOrder(root, k);
        }
    
        /**
         * 前序遍历
         * @param root
         * @param k
         */
        private void preOrder(TreeNode root, int k){
            if(root == null){
                return;
            }
    
            if(k == 0){
                list.add(root.val);
                return;
            }
    
            preOrder(root.left, k-1);
            preOrder(root.right, k-1);
        }
    }

  

