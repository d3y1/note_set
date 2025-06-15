# java-NC360 右侧更小数_2

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
    private SegNode[] segTree;

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
        // return solution4(nums);
        return solution44(nums);
    }

    /**
     * 线段树(Segment Tree): 数组实现(堆式存储)
     * @param nums
     * @return
     */
    private ArrayList<Integer> solution4(ArrayList<Integer> nums){
        n = nums.size();
        result = new int[n];
        segmentTree = new int[n*4+1];

        // 离散化处理
        discrete(nums);

        int num;
        // 从后往前遍历
        for(int i=n-1; i>=0; i--){
            num = nums.get(i);
            // 线段树id
            int id = getIdByNum(num);
            // 根据id获取区间和 严格小于(id-1) range: left<=right
            result[i] += querySum(0, id-1);
            // 更新前缀和
            change(id, 1);
        }

        ArrayList<Integer> list = new ArrayList<Integer>();
        for(int cnt : result){
            list.add(cnt);
        }

        return list;
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
    private ArrayList<Integer> solution44(ArrayList<Integer> nums){
        n = nums.size();
        result = new int[n];
        segTree = new SegNode[n*4+1];
        segTree[1] = new SegNode(0, n);

        // 离散化处理
        discrete(nums);

        int num;
        // 从后往前遍历
        for(int i=n-1; i>=0; i--){
            num = nums.get(i);
            // 线段树id
            int id = getIdByNum(num);
            // 根据id获取区间和 严格小于(id-1) range: left<=right
            result[i] += getSum(0, id-1);
            // 更新前缀和
            alter(id, 1);
        }

        ArrayList<Integer> list = new ArrayList<Integer>();
        for(int cnt : result){
            list.add(cnt);
        }

        return list;
    }

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