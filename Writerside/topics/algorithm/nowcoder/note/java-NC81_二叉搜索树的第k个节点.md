# java-NC81 二叉搜索树的第k个节点


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
     * NC81 二叉搜索树的第k个节点
     * @author d3y1
     */
    public class Solution {
        private int result = -1;
        private int K;
        
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param proot TreeNode类 
         * @param k int整型 
         * @return int整型
         */
        public int KthNode (TreeNode proot, int k) {
            // return solution1(proot, k);
            return solution2(proot, k);
        }
    
        private boolean found = false;
        private ArrayList<Integer> list = new ArrayList<>();
    
        /**
         * 中序遍历
         * @param proot
         * @param k
         * @return
         */
        private int solution1(TreeNode proot, int k){
            K = k;
            inOrder(proot);
            
            return result;
        }
    
        /**
         * 中序遍历(递归)
         * @param proot
         */
        private void inOrder(TreeNode proot){
            if(found){
                return;
            }
            if(proot == null){
                return;
            }
    
            inOrder(proot.left);
    
            list.add(proot.val);
            if(list.size() == K){
                found = true;
                result = proot.val;
                return;
            }
    
            inOrder(proot.right);
        }
        
        /////////////////////////////////////////////////////////////////////////////////////////
    
        private int seq = 0;
    
        /**
         * 中序遍历
         * @param proot
         * @param k
         * @return
         */
        private int solution2(TreeNode proot, int k){
            K = k;
            inorder(proot);
    
            return result;
        }
    
        /**
         * 中序遍历(递归)
         * @param proot
         */
        private void inorder(TreeNode proot){
            if(proot==null || seq>=K){
                return;
            }
            
            inorder(proot.left);
            if(++seq == K){
                result = proot.val;
            }
            inorder(proot.right);
        }
    }

  

