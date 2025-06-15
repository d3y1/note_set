# java-NC349 计算数组的小和

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
        // return solution1(nums);
        // return solution2(nums);
        // return solution3(nums);
        // return solution4(nums);
        // return solution44(nums);
        // return solution444(nums);
        return solution5(nums);
    }

    /**
     * 二分: 超时!
     * @param nums
     * @return
     */
    private long solution1(ArrayList<Integer> nums){
        long result = 0;
        int n = nums.size();

        ArrayList<Integer> list = new ArrayList<>();
        list.add(nums.get(0));

        // pos: 当前num(target)插入list位置(索引)
        int left,right,mid,last,target,pos,sum;
        for(int i=1; i<n; i++){
            last = list.get(i-1);
            target = nums.get(i);
            sum = 0;
            // 直接附加
            if(last <= target){
                pos = i;
                list.add(pos, target);
            }
            // 二分查找
            else{
                left = 0;
                right = i-1;
                while(left <= right){
                    mid = (left+right)>>1;
                    if(list.get(mid) <= target){
                        left = mid+1;
                    }else if(list.get(mid) > target){
                        right = mid-1;
                    }
                }

                pos = left;
                list.add(pos, target);
            }

            // 求和(小于等于当前num(target))
            for(int j=0; j<pos; j++){
                sum += list.get(j);
            }

            result += sum;
        }

        return result;
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 树状数组(Binary Indexed Tree)(也称Fenwick树): 动态维护前缀和
     *
     * 参考: https://www.bilibili.com/video/BV1pE41197Qj/?vd_source=fa6990445a0e68c4b18e85e07647ab23
     *
     * @param nums
     * @return
     */
    private long solution2(ArrayList<Integer> nums){
        long result = 0;
        int n = nums.size();

        // 离散化处理
        discrete(nums);

        // 初始化
        init(nums.size()+1);

        int num;
        for(int i=0; i<n; i++){
            num = nums.get(i);
            // 树状数组id
            int id = getIdByNum(num);
            // 根据id获取前缀和
            result += query(id);
            // 更新前缀和
            update(id, num);
        }

        return result;
    }

    /**
     * 初始化
     * @param length
     */
    private void init(int length) {
        t = new int[length];
        Arrays.fill(t, 0);
    }

    /**
     * 非负整数n在二进制表示下最低位1及后面的0所构成的数值
     *
     * 示例:
     * lowBit(44) = lowBit(101100[2进制]) = 100[2进制] = 4[10进制]
     *
     *         n    101100
     * 取反:   ~n    010011
     * 取反+1: ~n+1  010100
     *
     * ~n+1 = -n (计算机存储使用补码, 取反加1后的值即为负的这个数)
     *
     * lowBit(44) = n & (~n+1) = n & (-n)
     *
     * @param x
     * @return
     */
    private int lowBit(int x) {
        return x & (-x);
    }

    /**
     * 更新前缀和: 从当前节点往树根逐层更新父节点
     * @param pos
     * @param num
     */
    private void update(int pos, int num) {
        while (pos < t.length) {
            t[pos] += num;
            // 当前节点的父节点
            pos += lowBit(pos);
        }
    }

    /**
     * 查询前缀和: 从当前节点往左上逐个累加节点值
     * @param pos
     * @return
     */
    private long query(int pos) {
        long ret = 0;
        while (pos > 0) {
            ret += t[pos];
            // 当前节点的左上节点
            pos -= lowBit(pos);
        }

        return ret;
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 归并
     *
     * nums[i]最终累加次数 等价于 后面有多少个大于等于nums[i]的数(count[i])
     *
     * 示例:
     *   i   0 1 2 3 4 5
     * nums  1 3 5 2 4 6
     * count 5 3 1 2 1 0
     *
     * result = 1*5 + 3*3 + 5*1 + 2*2 + 4*1
     *        = 5 + 9 + 5 + 4 + 4
     *        = 27
     *
     * @param nums
     * @return
     */
    private long solution3(ArrayList<Integer> nums){
        Integer[] numsArr = new Integer[nums.size()];
        nums.toArray(numsArr);
        return mergeSort(numsArr, 0, nums.size()-1);
    }

    /**
     * 归并排序
     * @param nums
     * @param left
     * @param right
     * @return
     */
    private long mergeSort(Integer[] nums, int left, int right) {
        if(left >= right) {
            return 0;
        }

        int mid = left+((right-left)>>1);

        return mergeSort(nums, left, mid)+mergeSort(nums, mid+1, right)+merge(nums, left, mid, right);
    }

    /**
     * 合并
     * @param nums
     * @param left
     * @param mid
     * @param right
     * @return
     */
    private long merge(Integer[] nums, int left, int mid, int right) {
        long result = 0L;
        int[] help = new int[right-left+1];
        int i = 0;
        int p = left;
        int q = mid+1;
        while(p<=mid && q<=right) {
            result += (nums[p]<=nums[q]) ? nums[p]*(right-q+1) : 0;
            help[i++] = (nums[p]<=nums[q]) ? nums[p++] : nums[q++];
        }
        while(p <= mid) {
            help[i++] = nums[p++];
        }
        while(q <= right) {
            help[i++] = nums[q++];
        }
        for(i=0; i<help.length; i++) {
            nums[left+i] = help[i];
        }

        return result;
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 线段树(Segment Tree): 数组实现(堆式存储)
     * @param nums
     * @return
     */
    private long solution4(ArrayList<Integer> nums){
        n = nums.size();
        segmentTree = new int[n*4+1];
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
            result += rangeSum(0, id);
            // 更新前缀和
            modify(id, num);
        }

        return result;
    }

    /**
     * 更新: 根据id进行更新(单点修改)
     * @param id
     * @param val
     */
    public void modify(int id, int val) {
        modify(id, id, val, 0, 0, n);
    }

    /**
     * 递归: 更新线段树(区间修改)
     * @param left
     * @param right
     * @param val
     * @param root
     * @param start
     * @param end
     */
    private void modify(int left, int right, int val, int root, int start, int end){
        // [left, right]:   修改区间
        // [start, end]: 当前节点区间
        if(left<=start && end<=right){
            segmentTree[root] += (end-start+1)*val;
            return;
        }

        int mid = start+(end-start)/2;
        if(left <= mid){
            modify(left, right, val, root*2+1, start, mid);
        }
        if(right > mid){
            modify(left, right, val, root*2+2, mid+1, end);
        }

        segmentTree[root] = segmentTree[root*2+1]+segmentTree[root*2+2];
    }

    /**
     * 区间和(区间查询)
     * @param left
     * @param right
     * @return
     */
    public int rangeSum(int left, int right) {
        return rangeSum(left, right, 0, 0, n);
    }

    /**
     * 递归: 区间和
     * @param left
     * @param right
     * @param root
     * @param start
     * @param end
     * @return
     */
    private int rangeSum(int left, int right, int root, int start, int end){
        // [left, right]:   查询区间
        // [start, end]: 当前节点区间
        if(left<=start && end<=right){
            return segmentTree[root];
        }

        int mid = start+(end-start)/2;

        int sum = 0;
        if(left <= mid){
            sum += rangeSum(left, right, root*2+1, start, mid);
        }
        if(right > mid){
            sum += rangeSum(left, right, root*2+2, mid+1, end);
        }

        return sum;
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 线段树(Segment Tree): 数组实现(堆式存储)
     * @param nums
     * @return
     */
    private long solution44(ArrayList<Integer> nums){
        n = nums.size();
        segmentTree = new int[n*4+1];
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
            result += querySum(0, id);
            // 更新前缀和
            change(id, num);
        }

        return result;
    }

    /**
     * 更新: 根据id进行更新(单点修改)
     * @param id
     * @param val
     */
    public void change(int id, int val) {
        change(id, id, val, 1, 0, n);
    }

    /**
     * 递归: 更新线段树(区间修改)
     * @param left
     * @param right
     * @param val
     * @param root
     * @param start
     * @param end
     */
    private void change(int left, int right, int val, int root, int start, int end){
        // [left, right]:   修改区间
        // [start, end]: 当前节点区间
        if(left<=start && end<=right){
            segmentTree[root] += (end-start+1)*val;
            return;
        }

        int mid = start+(end-start)/2;
        if(left <= mid){
            change(left, right, val, root*2, start, mid);
        }
        if(right > mid){
            change(left, right, val, root*2+1, mid+1, end);
        }

        segmentTree[root] = segmentTree[root*2]+segmentTree[root*2+1];
    }

    /**
     * 区间和(区间查询)
     * @param left
     * @param right
     * @return
     */
    public int querySum(int left, int right) {
        return querySum(left, right, 1, 0, n);
    }

    /**
     * 递归: 区间和
     * @param left
     * @param right
     * @param root
     * @param start
     * @param end
     * @return
     */
    private int querySum(int left, int right, int root, int start, int end){
        // [left, right]:   查询区间
        // [start, end]: 当前节点区间
        if(left<=start && end<=right){
            return segmentTree[root];
        }

        int mid = start+(end-start)/2;

        int sum = 0;
        if(left <= mid){
            sum += querySum(left, right, root*2, start, mid);
        }
        if(right > mid){
            sum += querySum(left, right, root*2+1, mid+1, end);
        }

        return sum;
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////

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