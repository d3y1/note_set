# java-NC360 右侧更小数_1

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
        // return solution1(nums);
        // return solution2(nums);
        return solution3(nums);
    }

    /**
     * 二分
     * @param nums
     * @return
     */
    private ArrayList<Integer> solution1(ArrayList<Integer> nums){
        int n = nums.size();
        result = new int[n];

        ArrayList<Integer> list = new ArrayList<>();
        list.add(nums.get(n-1));

        // pos: 当前num(target)插入list位置(索引)
        int left,right,mid,last,target,pos,sum;
        for(int i=n-2; i>=0; i--){
            last = list.get(n-i-2);
            target = nums.get(i);
            // 直接附加
            if(last < target){
                pos = n-i-1;
                list.add(pos, target);
            }
            // 二分查找
            else{
                left = 0;
                right = n-i-2;
                while(left <= right){
                    mid = (left+right)>>1;
                    if(list.get(mid) < target){
                        left = mid+1;
                    }else{
                        right = mid-1;
                    }
                }

                pos = left;
                list.add(pos, target);
            }
            result[i] = pos;
        }

        ArrayList<Integer> arrayList = new ArrayList<>();
        for(int cnt : result){
            arrayList.add(cnt);
        }

        return arrayList;
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
    private ArrayList<Integer> solution2(ArrayList<Integer> nums){
        int n = nums.size();
        result = new int[n];

        // 离散化处理
        discrete(nums);

        // 初始化
        init(n+1);

        int num;
        // 从后往前遍历
        for(int i=n-1; i>=0; i--){
            num = nums.get(i);
            // 树状数组id
            int id = getIdByNum(num);
            // 根据id获取前缀和 严格小于(id-1)
            result[i] += query(id-1);
            // 更新前缀和
            update(id);
        }

        ArrayList<Integer> list = new ArrayList<Integer>();
        for(int cnt : result){
            list.add(cnt);
        }

        return list;
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
     */
    private void update(int pos) {
        while (pos < t.length) {
            // 新增1次
            t[pos] += 1;
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
     * 排序: 归并
     * @param nums
     * @return
     */
    private ArrayList<Integer> solution3(ArrayList<Integer> nums){
        int n = nums.size();

        Integer[] numsArr = new Integer[n];
        nums.toArray(numsArr);

        result = new int[n];
        idx = new int[n];
        for(int i=0; i<n; i++){
            idx[i] = i;
        }

        mergeSort(numsArr, 0, n-1);

        ArrayList<Integer> list = new ArrayList<Integer>();
        for(int cnt : result){
            list.add(cnt);
        }

        return list;
    }

    /**
     * 归并排序
     * @param nums
     * @param left
     * @param right
     * @return
     */
    private void mergeSort(Integer[] nums, int left, int right) {
        if(left >= right) {
            return;
        }

        int mid = left+((right-left)>>1);

        mergeSort(nums, left, mid);
        mergeSort(nums, mid+1, right);
        merge(nums, left, mid, right);
    }

    /**
     * 合并
     * @param nums
     * @param left
     * @param mid
     * @param right
     * @return
     */
    private void merge(Integer[] nums, int left, int mid, int right) {
        int len = right-left+1;
        int[] helpIdx = new int[len];
        int[] helpNum = new int[len];
        int i = 0;
        int p = left;
        int q = mid+1;
        while(p<=mid && q<=right) {
            if(nums[p] <= nums[q]){
                result[idx[p]] += q-mid-1;
                helpIdx[i] = idx[p];
                helpNum[i] = nums[p];
                i++;
                p++;
            }else{
                helpIdx[i] = idx[q];
                helpNum[i] = nums[q];
                i++;
                q++;
            }
        }
        while(p <= mid){
            result[idx[p]] += q-mid-1;
            helpIdx[i] = idx[p];
            helpNum[i] = nums[p];
            i++;
            p++;
        }
        while(q <= right){
            helpIdx[i] = idx[q];
            helpNum[i] = nums[q];
            i++;
            q++;
        }
        for(i=0; i<len; i++){
            idx[left+i] = helpIdx[i];
            nums[left+i] = helpNum[i];
        }
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
}
```