# java-NC349 计算数组的小和_3

```java
import java.util.*;

/**
 * NC349 计算数组的小和
 * @author d3y1
 */
public class Solution {
    // 树状数组t
    private int[] t;

    // 线段树
    private int[] segmentTree;

    // 离散化: 将nums离散化(去重+排序), 转化为数组d
    private int[] d;

    private int n;

    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 相似 -> NC360 右侧更小数 [nowcoder]
     *
     * 注意: 线段树lazy(懒惰标记)适用于区间修改(改善区间修改效率) -> https://oi-wiki.org/ds/seg/#线段树的区间修改与懒惰标记
     *
     * @param nums int整型ArrayList
     * @return long长整型
     */
    public long calArray (ArrayList<Integer> nums) {
        // return solution444(nums);
        return solution5(nums);
    }

    /**
     * 线段树(Segment Tree): 数组实现(堆式存储)
     * @param nums
     * @return
     */
    private long solution444(ArrayList<Integer> nums){
        n = nums.size();
        segTree = new SegNode[n*4+1];
        segTree[1] = new SegNode(0, n);
        long result = 0L;

        // 离散化处理
        discrete(nums);

        int num;
        // 从后往前遍历
        for(int i=0; i<n; i++){
            num = nums.get(i);
            // 线段树id
            int id = getIdByNum(num);
            // 根据id获取区间和 小于等于(id) range: left<=right
            result += getSum(0, id);
            // 更新前缀和
            alter(id, num);
        }

        return result;
    }

    // 线段树
    private SegNode[] segTree;

    /**
     * 更新: 根据id进行更新(单点修改)
     * @param id
     * @param val
     */
    public void alter(int id, int val) {
        alter(id, id, val, 1);
    }

    /**
     * 递归: 更新线段树(区间修改)
     * @param left
     * @param right
     * @param val
     * @param root
     */
    private void alter(int left, int right, int val, int root){
        // [left, right]:   修改区间
        // [start, end]: 当前节点区间
        if(left<=segTree[root].start && segTree[root].end<=right){
            segTree[root].sum += (segTree[root].end-segTree[root].start+1)*val;
            return;
        }

        int mid = segTree[root].start+(segTree[root].end-segTree[root].start)/2;

        if(segTree[root*2] == null){
            segTree[root*2] = new SegNode(segTree[root].start, mid);
        }
        if(segTree[root*2+1] == null){
            segTree[root*2+1] = new SegNode(mid+1, segTree[root].end);
        }

        if(left <= mid){
            alter(left, right, val, root*2);
        }
        if(right > mid){
            alter(left, right, val, root*2+1);
        }

        segTree[root].sum = segTree[root*2].sum+segTree[root*2+1].sum;
    }

    /**
     * 区间和(区间查询)
     * @param left
     * @param right
     * @return
     */
    public int getSum(int left, int right) {
        return getSum(left, right, 1);
    }

    /**
     * 递归: 区间和
     * @param left
     * @param right
     * @param root
     * @return
     */
    private int getSum(int left, int right, int root){
        // [left, right]:   查询区间
        // [start, end]: 当前节点区间
        if(left<=segTree[root].start && segTree[root].end<=right){
            return segTree[root].sum;
        }

        int mid = segTree[root].start+(segTree[root].end-segTree[root].start)/2;

        if(segTree[root*2] == null){
            segTree[root*2] = new SegNode(segTree[root].start, mid);
        }
        if(segTree[root*2+1] == null){
            segTree[root*2+1] = new SegNode(mid+1, segTree[root].end);
        }

        int sum = 0;
        if(left <= mid){
            sum += getSum(left, right, root*2);
        }
        if(right > mid){
            sum += getSum(left, right, root*2+1);
        }

        return sum;
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 线段树(Segment Tree): 树实现
     * @param nums
     * @return
     */
    private long solution5(ArrayList<Integer> nums){
        n = nums.size();
        TreeNode root = new TreeNode(0, n);
        long result = 0L;

        // 离散化处理
        discrete(nums);

        int num;
        // 从后往前遍历
        for(int i=0; i<n; i++){
            num = nums.get(i);
            // 线段树id
            int id = getIdByNum(num);
            // 根据id获取区间和 小于等于(id) range: left<=right
            result += rangeSum(root, 0, id);
            // 更新前缀和
            modify(root, id, num);
        }

        return result;
    }

    /**
     * 更新: 根据id进行更新(单点修改)
     * @param root
     * @param id
     * @param val
     */
    public void modify(TreeNode root, int id, int val) {
        modify(root, id, id, val);
    }

    /**
     * 递归: 更新线段树(区间修改)
     * @param root
     * @param left
     * @param right
     * @param val
     */
    private void modify(TreeNode root, int left, int right, int val) {
        if(left<=root.start && root.end<=right){
            root.sum += (root.end-root.start+1)*val;
            return;
        }

        int mid = root.start+(root.end-root.start)/2;
        if(root.left == null){
            root.left = new TreeNode(root.start, mid);
        }
        if(root.right == null){
            root.right = new TreeNode(mid+1, root.end);
        }

        if(left <= mid){
            modify(root.left, left, right, val);
        }
        if(right > mid){
            modify(root.right, left, right, val);
        }

        root.sum = root.left.sum+root.right.sum;
    }

    /**
     * 区间和(区间查询)
     * @param root
     * @param left
     * @param right
     * @return
     */
    public int rangeSum(TreeNode root, int left, int right) {
        if(root == null){
            return 0;
        }
        if(left<=root.start && root.end<=right){
            return root.sum;
        }

        int mid = root.start+(root.end-root.start)/2;
        if(root.left == null){
            root.left = new TreeNode(root.start, mid);
        }
        if(root.right == null){
            root.right = new TreeNode(mid+1, root.end);
        }

        int sum = 0;
        if(left <= mid){
            sum += rangeSum(root.left, left, right);
        }
        if(right > mid){
            sum += rangeSum(root.right, left, right);
        }

        return sum;
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 离散化处理
     *
     * nums数组中可能有负数或者可能稀疏 -> 离散化处理
     *
     * @param nums
     */
    private void discrete(ArrayList<Integer> nums) {
        Set<Integer> set = new HashSet<>(nums);
        int size = set.size();
        d = new int[size];
        int index = 0;
        for(int num : set){
            d[index++] = num;
        }
        Arrays.sort(d);
    }

    /**
     * 二分: 根据num获取树状数组id (num -> id)
     * @param num
     * @return
     */
    private int getIdByNum(int num) {
        return Arrays.binarySearch(d, num)+1;
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////

    private class TreeNode {
        // 区间
        int start,end;
        int sum = 0;
        TreeNode left = null;
        TreeNode right = null;

        public TreeNode(int start, int end) {
            this.start = start;
            this.end = end;
        }
    }

    private class SegNode {
        private int start;
        private int end;
        private int sum = 0;

        public SegNode(int start, int end){
            this.start = start;
            this.end = end;
        }
    }
}
```