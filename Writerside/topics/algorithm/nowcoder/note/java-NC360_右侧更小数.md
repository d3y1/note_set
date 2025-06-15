# java-NC360 右侧更小数


    import java.util.*;
    
    /**
     * NC360 右侧更小数
     * @author d3y1
     */
    public class Solution {
        // 树状数组t
        private int[] t;
    
        // 线段树
        private int[] segmentTree;
        private SegNode[] segTree;
    
        // 离散化: 将nums离散化(去重+排序), 转化为数组d
        private int[] d;
    
        // 归并
        private int[] idx;
        
        private int n;
        private int[] result;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相同 -> 315    计算右侧小于当前元素的个数   [leetcode]
         * 相似 -> NC349  计算数组的小和             [nowcoder]
         *
         * 注意: 线段树lazy(懒惰标记)适用于区间修改(改善区间修改效率) -> https://oi-wiki.org/ds/seg/#线段树的区间修改与懒惰标记
         *
         * @param nums int整型ArrayList
         * @return int整型ArrayList
         */
        public ArrayList<Integer> smallerCount (ArrayList<Integer> nums) {
            // return solution1(nums);
            // return solution2(nums);
            // return solution3(nums);
            // return solution4(nums);
            // return solution44(nums);
            // return solution444(nums);
            // return solution4444(nums);
            // return solution5(nums);
            return solution55(nums);
        }
    
        /**
         * 二分
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution1(ArrayList<Integer> nums){
            int n = nums.size();
            result = new int[n];
    
            ArrayList<Integer> list = new ArrayList<>();
            list.add(nums.get(n-1));
    
            // pos: 当前num(target)插入list位置(索引)
            int left,right,mid,last,target,pos,sum;
            for(int i=n-2; i>=0; i--){
                last = list.get(n-i-2);
                target = nums.get(i);
                // 直接附加
                if(last < target){
                    pos = n-i-1;
                    list.add(pos, target);
                }
                // 二分查找
                else{
                    left = 0;
                    right = n-i-2;
                    while(left <= right){
                        mid = (left+right)>>1;
                        if(list.get(mid) < target){
                            left = mid+1;
                        }else{
                            right = mid-1;
                        }
                    }
    
                    pos = left;
                    list.add(pos, target);
                }
                result[i] = pos;
            }
    
            ArrayList<Integer> arrayList = new ArrayList<>();
            for(int cnt : result){
                arrayList.add(cnt);
            }
    
            return arrayList;
        }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 树状数组(Binary Indexed Tree)(也称Fenwick树): 动态维护前缀和
         *
         * 参考: https://www.bilibili.com/video/BV1pE41197Qj/?vd_source=fa6990445a0e68c4b18e85e07647ab23
         *
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution2(ArrayList<Integer> nums){
            int n = nums.size();
            result = new int[n];
    
            // 离散化处理
            discrete(nums);
    
            // 初始化
            init(n+1);
    
            int num;
            // 从后往前遍历
            for(int i=n-1; i>=0; i--){
                num = nums.get(i);
                // 树状数组id
                int id = getIdByNum(num);
                // 根据id获取前缀和 严格小于(id-1)
                result[i] += query(id-1);
                // 更新前缀和
                update(id);
            }
    
            ArrayList<Integer> list = new ArrayList<Integer>();
            for(int cnt : result){
                list.add(cnt);
            }
    
            return list;
        }
    
        /**
         * 初始化
         * @param length
         */
        private void init(int length) {
            t = new int[length];
            Arrays.fill(t, 0);
        }
    
        /**
         * 非负整数n在二进制表示下最低位1及后面的0所构成的数值
         *
         * 示例:
         * lowBit(44) = lowBit(101100[2进制]) = 100[2进制] = 4[10进制]
         *
         *         n    101100
         * 取反:   ~n    010011
         * 取反+1: ~n+1  010100
         *
         * ~n+1 = -n (计算机存储使用补码, 取反加1后的值即为负的这个数)
         *
         * lowBit(44) = n & (~n+1) = n & (-n)
         *
         * @param x
         * @return
         */
        private int lowBit(int x) {
            return x & (-x);
        }
    
        /**
         * 更新前缀和: 从当前节点往树根逐层更新父节点
         * @param pos
         */
        private void update(int pos) {
            while (pos < t.length) {
                // 新增1次
                t[pos] += 1;
                // 当前节点的父节点
                pos += lowBit(pos);
            }
        }
    
        /**
         * 查询前缀和: 从当前节点往左上逐个累加节点值
         * @param pos
         * @return
         */
        private long query(int pos) {
            long ret = 0;
            while (pos > 0) {
                ret += t[pos];
                // 当前节点的左上节点
                pos -= lowBit(pos);
            }
    
            return ret;
        }
        
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 排序: 归并
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution3(ArrayList<Integer> nums){
            int n = nums.size();
    
            Integer[] numsArr = new Integer[n];
            nums.toArray(numsArr);
    
            result = new int[n];
            idx = new int[n];
            for(int i=0; i<n; i++){
                idx[i] = i;
            }
    
            mergeSort(numsArr, 0, n-1);
    
            ArrayList<Integer> list = new ArrayList<Integer>();
            for(int cnt : result){
                list.add(cnt);
            }
    
            return list;
        }
    
        /**
         * 归并排序
         * @param nums
         * @param left
         * @param right
         * @return
         */
        private void mergeSort(Integer[] nums, int left, int right) {
            if(left >= right) {
                return;
            }
    
            int mid = left+((right-left)>>1);
    
            mergeSort(nums, left, mid);
            mergeSort(nums, mid+1, right);
            merge(nums, left, mid, right);
        }
    
        /**
         * 合并
         * @param nums
         * @param left
         * @param mid
         * @param right
         * @return
         */
        private void merge(Integer[] nums, int left, int mid, int right) {
            int len = right-left+1;
            int[] helpIdx = new int[len];
            int[] helpNum = new int[len];
            int i = 0;
            int p = left;
            int q = mid+1;
            while(p<=mid && q<=right) {
                if(nums[p] <= nums[q]){
                    result[idx[p]] += q-mid-1;
                    helpIdx[i] = idx[p];
                    helpNum[i] = nums[p];
                    i++;
                    p++;
                }else{
                    helpIdx[i] = idx[q];
                    helpNum[i] = nums[q];
                    i++;
                    q++;
                }
            }
            while(p <= mid){
                result[idx[p]] += q-mid-1;
                helpIdx[i] = idx[p];
                helpNum[i] = nums[p];
                i++;
                p++;
            }
            while(q <= right){
                helpIdx[i] = idx[q];
                helpNum[i] = nums[q];
                i++;
                q++;
            }
            for(i=0; i<len; i++){
                idx[left+i] = helpIdx[i];
                nums[left+i] = helpNum[i];
            }
        }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        // /**
        //  * 线段树(Segment Tree): 数组实现(堆式存储)
        //  * @param nums
        //  * @return
        //  */
        // private ArrayList<Integer> solution4(ArrayList<Integer> nums){
        //     n = nums.size();
        //     result = new int[n];
        //     segmentTree = new int[n*4];
    
        //     // 离散化处理
        //     discrete(nums);
    
        //     int num;
        //     // 从后往前遍历
        //     for(int i=n-1; i>=0; i--){
        //         num = nums.get(i);
        //         // 线段树id
        //         int id = getIdByNum(num);
        //         // 根据id获取区间和 严格小于(id-1) range: left<=right
        //         result[i] += sumRange(0, id-1);
        //         // 更新前缀和
        //         update(id, 1);
        //     }
    
        //     ArrayList<Integer> list = new ArrayList<Integer>();
        //     for(int cnt : result){
        //         list.add(cnt);
        //     }
    
        //     return list;
        // }
    
        // /**
        //  * 更新: 根据id进行更新
        //  * @param id
        //  * @param val
        //  */
        // public void update(int id, int val) {
        //     change(id, val, 0, 0, n);
        // }
    
        // /**
        //  * 区间和
        //  * @param left
        //  * @param right
        //  * @return
        //  */
        // public int sumRange(int left, int right) {
        //     return range(left, right, 0, 0, n);
        // }
    
        // /**
        //  * 递归: 更新线段树
        //  * @param index
        //  * @param val
        //  * @param node
        //  * @param start
        //  * @param end
        //  */
        // private void change(int index, int val, int node, int start, int end) {
        //     if(start == end){
        //         segmentTree[node] += val;
        //         return;
        //     }
        //     int mid = start+(end-start)/2;
        //     if(index <= mid){
        //         change(index, val, node*2+1, start, mid);
        //     }else{
        //         change(index, val, node*2+2, mid+1, end);
        //     }
        //     segmentTree[node] = segmentTree[node*2+1]+segmentTree[node*2+2];
        // }
    
        // /**
        //  * 递归: 区间和
        //  * @param left
        //  * @param right
        //  * @param node
        //  * @param start
        //  * @param end
        //  * @return
        //  */
        // private int range(int left, int right, int node, int start, int end) {
        //     if(left==start && right==end){
        //         return segmentTree[node];
        //     }
        //     int mid = start+(end-start)/2;
        //     if(right <= mid){
        //         return range(left, right, node*2+1, start, mid);
        //     }else if(left > mid){
        //         return range(left, right, node*2+2, mid+1, end);
        //     }else{
        //         return range(left, mid, node*2+1, start, mid) + range(mid+1, right, node*2+2, mid+1, end);
        //     }
        // }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 线段树(Segment Tree): 数组实现(堆式存储)
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution44(ArrayList<Integer> nums){
            n = nums.size();
            result = new int[n];
            segmentTree = new int[n*4+1];
    
            // 离散化处理
            discrete(nums);
    
            int num;
            // 从后往前遍历
            for(int i=n-1; i>=0; i--){
                num = nums.get(i);
                // 线段树id
                int id = getIdByNum(num);
                // 根据id获取区间和 严格小于(id-1) range: left<=right
                result[i] += rangeSum(0, id-1);
                // 更新前缀和
                modify(id, 1);
            }
    
            ArrayList<Integer> list = new ArrayList<Integer>();
            for(int cnt : result){
                list.add(cnt);
            }
    
            return list;
        }
    
        /**
         * 更新: 根据id进行更新(单点修改)
         * @param id
         * @param val
         */
        public void modify(int id, int val) {
            modify(id, id, val, 0, 0, n);
        }
    
        /**
         * 递归: 更新线段树(区间修改)
         * @param left
         * @param right
         * @param val
         * @param root
         * @param start
         * @param end
         */
        private void modify(int left, int right, int val, int root, int start, int end){
            // [left, right]:   修改区间
            // [start, end]: 当前节点区间
            if(left<=start && end<=right){
                segmentTree[root] += (end-start+1)*val;
                return;
            }
    
            int mid = start+(end-start)/2;
            if(left <= mid){
                modify(left, right, val, root*2+1, start, mid);
            }
            if(right > mid){
                modify(left, right, val, root*2+2, mid+1, end);
            }
    
            segmentTree[root] = segmentTree[root*2+1]+segmentTree[root*2+2];
        }
    
        /**
         * 区间和(区间查询)
         * @param left
         * @param right
         * @return
         */
        public int rangeSum(int left, int right) {
            return rangeSum(left, right, 0, 0, n);
        }
    
        /**
         * 递归: 区间和
         * @param left
         * @param right
         * @param root
         * @param start
         * @param end
         * @return
         */
        private int rangeSum(int left, int right, int root, int start, int end){
            // [left, right]:   查询区间
            // [start, end]: 当前节点区间
            if(left<=start && end<=right){
                return segmentTree[root];
            }
    
            int mid = start+(end-start)/2;
    
            int sum = 0;
            if(left <= mid){
                sum += rangeSum(left, right, root*2+1, start, mid);
            }
            if(right > mid){
                sum += rangeSum(left, right, root*2+2, mid+1, end);
            }
    
            return sum;
        }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 线段树(Segment Tree): 数组实现(堆式存储)
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution444(ArrayList<Integer> nums){
            n = nums.size();
            result = new int[n];
            segmentTree = new int[n*4+1];
    
            // 离散化处理
            discrete(nums);
    
            int num;
            // 从后往前遍历
            for(int i=n-1; i>=0; i--){
                num = nums.get(i);
                // 线段树id
                int id = getIdByNum(num);
                // 根据id获取区间和 严格小于(id-1) range: left<=right
                result[i] += querySum(0, id-1);
                // 更新前缀和
                change(id, 1);
            }
    
            ArrayList<Integer> list = new ArrayList<Integer>();
            for(int cnt : result){
                list.add(cnt);
            }
    
            return list;
        }
    
        /**
         * 更新: 根据id进行更新(单点修改)
         * @param id
         * @param val
         */
        public void change(int id, int val) {
            change(id, id, val, 1, 0, n);
        }
    
        /**
         * 递归: 更新线段树(区间修改)
         * @param left
         * @param right
         * @param val
         * @param root
         * @param start
         * @param end
         */
        private void change(int left, int right, int val, int root, int start, int end){
            // [left, right]:   修改区间
            // [start, end]: 当前节点区间
            if(left<=start && end<=right){
                segmentTree[root] += (end-start+1)*val;
                return;
            }
    
            int mid = start+(end-start)/2;
            if(left <= mid){
                change(left, right, val, root*2, start, mid);
            }
            if(right > mid){
                change(left, right, val, root*2+1, mid+1, end);
            }
    
            segmentTree[root] = segmentTree[root*2]+segmentTree[root*2+1];
        }
    
        /**
         * 区间和(区间查询)
         * @param left
         * @param right
         * @return
         */
        public int querySum(int left, int right) {
            return querySum(left, right, 1, 0, n);
        }
    
        /**
         * 递归: 区间和
         * @param left
         * @param right
         * @param root
         * @param start
         * @param end
         * @return
         */
        private int querySum(int left, int right, int root, int start, int end){
            // [left, right]:   查询区间
            // [start, end]: 当前节点区间
            if(left<=start && end<=right){
                return segmentTree[root];
            }
    
            int mid = start+(end-start)/2;
    
            int sum = 0;
            if(left <= mid){
                sum += querySum(left, right, root*2, start, mid);
            }
            if(right > mid){
                sum += querySum(left, right, root*2+1, mid+1, end);
            }
    
            return sum;
        }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 线段树(Segment Tree): 数组实现(堆式存储)
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution4444(ArrayList<Integer> nums){
            n = nums.size();
            result = new int[n];
            segTree = new SegNode[n*4+1];
            segTree[1] = new SegNode(0, n);
    
            // 离散化处理
            discrete(nums);
    
            int num;
            // 从后往前遍历
            for(int i=n-1; i>=0; i--){
                num = nums.get(i);
                // 线段树id
                int id = getIdByNum(num);
                // 根据id获取区间和 严格小于(id-1) range: left<=right
                result[i] += getSum(0, id-1);
                // 更新前缀和
                alter(id, 1);
            }
    
            ArrayList<Integer> list = new ArrayList<Integer>();
            for(int cnt : result){
                list.add(cnt);
            }
    
            return list;
        }
    
        /**
         * 更新: 根据id进行更新(单点修改)
         * @param id
         * @param val
         */
        public void alter(int id, int val) {
            alter(id, id, val, 1);
        }
    
        /**
         * 递归: 更新线段树(区间修改)
         * @param left
         * @param right
         * @param val
         * @param root
         */
        private void alter(int left, int right, int val, int root){
            // [left, right]:   修改区间
            // [start, end]: 当前节点区间
            if(left<=segTree[root].start && segTree[root].end<=right){
                segTree[root].sum += (segTree[root].end-segTree[root].start+1)*val;
                return;
            }
    
            int mid = segTree[root].start+(segTree[root].end-segTree[root].start)/2;
    
            if(segTree[root*2] == null){
                segTree[root*2] = new SegNode(segTree[root].start, mid);
            }
            if(segTree[root*2+1] == null){
                segTree[root*2+1] = new SegNode(mid+1, segTree[root].end);
            }
    
            if(left <= mid){
                alter(left, right, val, root*2);
            }
            if(right > mid){
                alter(left, right, val, root*2+1);
            }
    
            segTree[root].sum = segTree[root*2].sum+segTree[root*2+1].sum;
        }
    
        /**
         * 区间和(区间查询)
         * @param left
         * @param right
         * @return
         */
        public int getSum(int left, int right) {
            return getSum(left, right, 1);
        }
    
        /**
         * 递归: 区间和
         * @param left
         * @param right
         * @param root
         * @return
         */
        private int getSum(int left, int right, int root){
            // [left, right]:   查询区间
            // [start, end]: 当前节点区间
            if(left<=segTree[root].start && segTree[root].end<=right){
                return segTree[root].sum;
            }
    
            int mid = segTree[root].start+(segTree[root].end-segTree[root].start)/2;
    
            if(segTree[root*2] == null){
                segTree[root*2] = new SegNode(segTree[root].start, mid);
            }
            if(segTree[root*2+1] == null){
                segTree[root*2+1] = new SegNode(mid+1, segTree[root].end);
            }
    
            int sum = 0;
            if(left <= mid){
                sum += getSum(left, right, root*2);
            }
            if(right > mid){
                sum += getSum(left, right, root*2+1);
            }
    
            return sum;
        }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        // /**
        //  * 线段树(Segment Tree): 树实现
        //  * @param nums
        //  * @return
        //  */
        // private ArrayList<Integer> solution5(ArrayList<Integer> nums){
        //     n = nums.size();
        //     result = new int[n];
        //     TreeNode root = new TreeNode(0, n);
    
        //     // 离散化处理
        //     discrete(nums);
    
        //     int num;
        //     // 从后往前遍历
        //     for(int i=n-1; i>=0; i--){
        //         num = nums.get(i);
        //         // 线段树id
        //         int id = getIdByNum(num);
        //         // 根据id获取区间和 严格小于(id-1) range: left<=right
        //         result[i] += sumRange(root, 0, id-1);
        //         // 更新前缀和
        //         update(root, id, 1);
        //     }
    
        //     ArrayList<Integer> list = new ArrayList<Integer>();
        //     for(int cnt : result){
        //         list.add(cnt);
        //     }
    
        //     return list;
        // }
    
        // /**
        //  * 更新: 根据id进行更新
        //  * @param root
        //  * @param id
        //  * @param val
        //  */
        // public void update(TreeNode root, int id, int val) {
        //     change(root, id, val);
        // }
    
        // /**
        //  * 递归: 更新线段树
        //  * @param root
        //  * @param index
        //  * @param val
        //  */
        // private void change(TreeNode root, int index, int val) {
        //     if(root.start == root.end){
        //         root.sum += val;
        //         return;
        //     }
    
        //     int mid = root.start+(root.end-root.start)/2;
        //     if(root.left == null){
        //         root.left = new TreeNode(root.start, mid);
        //     }
        //     if(root.right == null){
        //         root.right = new TreeNode(mid+1, root.end);
        //     }
    
        //     if(index <= mid){
        //         change(root.left, index, val);
        //     }else{
        //         change(root.right, index, val);
        //     }
    
        //     root.sum = root.left.sum+root.right.sum;
        // }
    
        // /**
        //  * 区间和
        //  * @param root
        //  * @param left
        //  * @param right
        //  * @return
        //  */
        // public int sumRange(TreeNode root, int left, int right) {
        //     return range(root, left, right);
        // }
    
        // /**
        //  * 递归: 区间和
        //  * @param root
        //  * @param left
        //  * @param right
        //  * @return
        //  */
        // private int range(TreeNode root, int left, int right) {
        //     if(root == null){
        //         return 0;
        //     }
        //     if(left==root.start && right==root.end){
        //         return root.sum;
        //     }
    
        //     int mid = root.start+(root.end-root.start)/2;
        //     if(root.left == null){
        //         root.left = new TreeNode(root.start, mid);
        //     }
        //     if(root.right == null){
        //         root.right = new TreeNode(mid+1, root.end);
        //     }
    
        //     if(right <= mid){
        //         return range(root.left, left, right);
        //     }else if(left > mid){
        //         return range(root.right, left, right);
        //     }else{
        //         return range(root.left, left, mid)+range(root.right, mid+1, right);
        //     }
        // }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 线段树(Segment Tree): 树实现
         * @param nums
         * @return
         */
        private ArrayList<Integer> solution55(ArrayList<Integer> nums){
            n = nums.size();
            result = new int[n];
            TreeNode root = new TreeNode(0, n);
    
            // 离散化处理
            discrete(nums);
    
            int num;
            // 从后往前遍历
            for(int i=n-1; i>=0; i--){
                num = nums.get(i);
                // 线段树id
                int id = getIdByNum(num);
                // 根据id获取区间和 严格小于(id-1) range: left<=right
                result[i] += rangeSum(root, 0, id-1);
                // 更新前缀和
                modify(root, id, 1);
            }
    
            ArrayList<Integer> list = new ArrayList<Integer>();
            for(int cnt : result){
                list.add(cnt);
            }
    
            return list;
        }
    
        /**
         * 更新: 根据id进行更新(单点修改)
         * @param root
         * @param id
         * @param val
         */
        public void modify(TreeNode root, int id, int val) {
            modify(root, id, id, val);
        }
    
        /**
         * 递归: 更新线段树(区间修改)
         * @param root
         * @param left
         * @param right
         * @param val
         */
        private void modify(TreeNode root, int left, int right, int val) {
            if(left<=root.start && root.end<=right){
                root.sum += (root.end-root.start+1)*val;
                return;
            }
    
            int mid = root.start+(root.end-root.start)/2;
            if(root.left == null){
                root.left = new TreeNode(root.start, mid);
            }
            if(root.right == null){
                root.right = new TreeNode(mid+1, root.end);
            }
    
            if(left <= mid){
                modify(root.left, left, right, val);
            }
            if(right > mid){
                modify(root.right, left, right, val);
            }
    
            root.sum = root.left.sum+root.right.sum;
        }
    
        /**
         * 区间和(区间查询)
         * @param root
         * @param left
         * @param right
         * @return
         */
        public int rangeSum(TreeNode root, int left, int right) {
            if(root == null){
                return 0;
            }
            if(left<=root.start && root.end<=right){
                return root.sum;
            }
    
            int mid = root.start+(root.end-root.start)/2;
            if(root.left == null){
                root.left = new TreeNode(root.start, mid);
            }
            if(root.right == null){
                root.right = new TreeNode(mid+1, root.end);
            }
    
            int sum = 0;
            if(left <= mid){
                sum += rangeSum(root.left, left, right);
            }
            if(right > mid){
                sum += rangeSum(root.right, left, right);
            }
    
            return sum;
        }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 离散化处理
         *
         * nums数组中可能有负数或者可能稀疏 -> 离散化处理
         *
         * @param nums
         */
        private void discrete(ArrayList<Integer> nums) {
            Set<Integer> set = new HashSet<>(nums);
            int size = set.size();
            d = new int[size];
            int index = 0;
            for(int num : set){
                d[index++] = num;
            }
            Arrays.sort(d);
        }
    
        /**
         * 二分: 根据num获取树状数组id (num -> id)
         * @param num
         * @return
         */
        private int getIdByNum(int num) {
            return Arrays.binarySearch(d, num)+1;
        }
    
        /////////////////////////////////////////////////////////////////////////////////////////////////////
    
        public class TreeNode {
            // 区间
            int start,end;
            int sum = 0;
            TreeNode left = null;
            TreeNode right = null;
    
            public TreeNode(int start, int end) {
                this.start = start;
                this.end = end;
            }
        }
    
        private class SegNode {
            private int start;
            private int end;
            private int sum = 0;
    
            public SegNode(int start, int end){
                this.start = start;
                this.end = end;
            }
        }
    }

  

