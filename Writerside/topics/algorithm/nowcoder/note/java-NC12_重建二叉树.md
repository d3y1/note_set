# java-NC12 重建二叉树

```java
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
 * NC12 重建二叉树
 * @author d3y1
 */
public class Solution {
    HashMap<Integer,Integer> inMap = new HashMap<>();

    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 相似 -> NC223 从中序与后序遍历序列构造二叉树 [nowcoder]
     *
     * @param preOrder int整型一维数组
     * @param vinOrder int整型一维数组
     * @return TreeNode类
     */
    public TreeNode reConstructBinaryTree (int[] preOrder, int[] vinOrder) {
        // return solution1(preOrder, vinOrder);
        // return solution2(preOrder, vinOrder);
        // return solution22(preOrder, vinOrder);
        return solution3(preOrder, vinOrder);
    }

    /**
     * 递归
     * @param preOrder
     * @param vinOrder
     * @return
     */
    private TreeNode solution1(int[] preOrder, int[] vinOrder){
        return construct(preOrder, vinOrder);
    }

    /**
     * 递归
     * @param preOrder
     * @param vinOrder
     * @return
     */
    public TreeNode construct(int[] preOrder, int[] vinOrder){
        int n = preOrder.length;
        if(n == 0){
            return null;
        }
        // 当前根结点
        int rootVal = preOrder[0];
        TreeNode root = new TreeNode(rootVal);
        // 当前根结点 左子树节点个数
        int left = 0;
        while(vinOrder[left] != rootVal){
            left++;
        }
        if(left > 0){
            // int[] pre = new int[left];
            // int[] vin = new int[left];
            // System.arraycopy(preOrder, 1, pre, 0, left);
            // System.arraycopy(vinOrder, 0, vin, 0, left);
            // root.left = construct(pre, vin);

            root.left = construct(Arrays.copyOfRange(preOrder, 1, left+1), Arrays.copyOfRange(vinOrder, 0, left));
        }
        // 当前根结点 右子树节点个数
        int right = n-(left+1);
        if(right > 0){
            // int[] pre = new int[right];
            // int[] vin = new int[right];
            // System.arraycopy(preOrder, left+1, pre, 0, right);
            // System.arraycopy(vinOrder, left+1, vin, 0, right);
            // root.right = construct(pre, vin);

            root.right = construct(Arrays.copyOfRange(preOrder, left+1, n), Arrays.copyOfRange(vinOrder, left+1, n));
        }

        return root;
    }

    //////////////////////////////////////////////////////////////////////////////////////

    /**
     * 哈希 + 递归
     * @param preOrder
     * @param vinOrder
     * @return
     */
    private TreeNode solution2(int[] preOrder, int[] vinOrder){
        int n = vinOrder.length;
        if(n == 0){
            return null;
        }

        // 哈希: val -> idx
        for(int i=0; i<n; i++){
            inMap.put(vinOrder[i], i);
        }

        // 根结点
        TreeNode root = new TreeNode(preOrder[0]);
        // 递归遍历
        dfs(preOrder, root, 0, n-1, 0, n-1);

        return root;
    }

    /**
     * 递归遍历
     * @param preOrder
     * @param root
     * @param inLeft
     * @param inRight
     * @param preLeft
     * @param preRight
     */
    private void dfs(int[] preOrder, TreeNode root, int inLeft, int inRight, int preLeft, int preRight){
        int inRootIdx = inMap.get(root.val);

        int leftSize = inRootIdx-inLeft;
        int rightSize = inRight-inRootIdx;

        // 有左子树
        if(leftSize > 0){
            root.left = new TreeNode(preOrder[preLeft+1]);
            dfs(preOrder, root.left, inLeft, inRootIdx-1, preLeft+1, preLeft+leftSize);
        }

        // 有右子树
        if(rightSize > 0){
            root.right = new TreeNode(preOrder[preLeft+leftSize+1]);
            dfs(preOrder, root.right, inRootIdx+1, inRight, preLeft+leftSize+1, preRight);
        }
    }

    //////////////////////////////////////////////////////////////////////////////////////

    /**
     * 哈希+递归: 简化
     * @param preOrder
     * @param vinOrder
     * @return
     */
    private TreeNode solution22(int[] preOrder, int[] vinOrder){
        int n = vinOrder.length;
        if(n == 0){
            return null;
        }

        // 哈希: val -> idx
        for(int i=0; i<n; i++){
            inMap.put(vinOrder[i], i);
        }

        // 递归遍历
        return dfs(preOrder, 0, n-1, 0, n-1);
    }

    /**
     * 递归遍历: 简化
     * @param preOrder
     * @param inLeft
     * @param inRight
     * @param preLeft
     * @param preRight
     */
    private TreeNode dfs(int[] preOrder, int inLeft, int inRight, int preLeft, int preRight){
        TreeNode root = new TreeNode(preOrder[preLeft]);

        int inRootIdx = inMap.get(root.val);

        int leftSize = inRootIdx-inLeft;
        int rightSize = inRight-inRootIdx;

        // 有左子树
        if(leftSize > 0){
            root.left = dfs(preOrder, inLeft, inRootIdx-1, preLeft+1, preLeft+leftSize);
        }

        // 有右子树
        if(rightSize > 0){
            root.right = dfs(preOrder, inRootIdx+1, inRight, preLeft+leftSize+1, preRight);
        }

        return root;
    }

    //////////////////////////////////////////////////////////////////////////////////////

    // 前序遍历根结点索引
    private int preRootIdx;

    /**
     * 哈希 + 递归
     * @param preOrder
     * @param vinOrder
     * @return
     */
    private TreeNode solution3(int[] preOrder, int[] vinOrder){
        int n = preOrder.length;
        preRootIdx = 0;

        // 哈希: val -> idx
        for(int i=0; i<n; i++){
            inMap.put(vinOrder[i], i);
        }

        return build(preOrder, 0, n-1);
    }

    /**
     * 递归遍历
     *
     * 二叉树前序遍历: 根 -> 左 -> 右
     * 可利用该性质直接找到前序遍历根节点, 子树遍历先左后右: 左 -> 右
     *
     * @param preOrder
     * @param inLeft
     * @param inRight
     * @return
     */
    private TreeNode build(int[] preOrder, int inLeft, int inRight){
        if(inLeft > inRight){
            return null;
        }

        // 根
        int preRootVal = preOrder[preRootIdx++];
        TreeNode root = new TreeNode(preRootVal);

        if(inLeft == inRight){
            return root;
        }

        // 中序遍历根结点索引
        int inRootIdx = inMap.get(preRootVal);

        // 左
        root.left = build(preOrder, inLeft, inRootIdx-1);
        // 右
        root.right = build(preOrder, inRootIdx+1, inRight);


        return root;
    }
}
```
