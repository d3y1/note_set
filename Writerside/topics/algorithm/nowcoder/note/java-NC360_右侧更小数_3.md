# java-NC360 右侧更小数_3

```java
import java.util.*;

/**
 * NC360 右侧更小数
 * @author d3y1
 */
public class Solution {
    // 树状数组t
    private int[] t;

    // 线段树
    private int[] segmentTree;

    // 离散化: 将nums离散化(去重+排序), 转化为数组d
    private int[] d;

    // 归并
    private int[] idx;

    private int n;
    private int[] result;

    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 相同 -> 315    计算右侧小于当前元素的个数   [leetcode]
     * 相似 -> NC349  计算数组的小和             [nowcoder]
     *
     * 注意: 线段树lazy(懒惰标记)适用于区间修改(改善区间修改效率) -> https://oi-wiki.org/ds/seg/#线段树的区间修改与懒惰标记
     *
     * @param nums int整型ArrayList
     * @return int整型ArrayList
     */
    public ArrayList<Integer> smallerCount (ArrayList<Integer> nums) {
        return solution5(nums);
    }

    /**
     * 线段树(Segment Tree): 树实现
     * @param nums
     * @return
     */
    private ArrayList<Integer> solution5(ArrayList<Integer> nums){
        n = nums.size();
        result = new int[n];
        TreeNode root = new TreeNode(0, n);

        // 离散化处理
        discrete(nums);

        int num;
        // 从后往前遍历
        for(int i=n-1; i>=0; i--){
            num = nums.get(i);
            // 线段树id
            int id = getIdByNum(num);
            // 根据id获取区间和 严格小于(id-1) range: left<=right
            result[i] += rangeSum(root, 0, id-1);
            // 更新前缀和
            modify(root, id, 1);
        }

        ArrayList<Integer> list = new ArrayList<Integer>();
        for(int cnt : result){
            list.add(cnt);
        }

        return list;
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

    public class TreeNode {
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
}
```