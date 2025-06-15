# java-NC408 第 K 小的距离对


    import java.util.*;
    
    /**
     * NC408 第 K 小的距离对
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC357 矩阵第K小    [nowcoder]
         *
         * @param nums int整型ArrayList
         * @param k int整型
         * @return int整型
         */
        public int kthDistance (ArrayList<Integer> nums, int k) {
            // return solution1(nums, k);
            // return solution2(nums, k);
            return solution3(nums, k);
        }
    
        /**
         * 双指针+排序: 超时!
         * @param nums
         * @param k
         * @return
         */
        private int solution1(ArrayList<Integer> nums, int k){
            int n = nums.size();
    
            int size = n*(n-1)/2;
            int[] dist = new int[size];
    
            int idx = 0;
            // 双指针
            for(int i=0; i<n; i++){
                for(int j=i+1; j<n; j++){
                    dist[idx++] = Math.abs(nums.get(i)-nums.get(j));
                }
            }
    
            // 排序
            Arrays.sort(dist);
    
            return dist[k-1];
        }
    
        /**
         * 双指针+二分: 超时!
         * @param nums
         * @param k
         * @return
         */
        private int solution2(ArrayList<Integer> nums, int k){
            int n = nums.size();
    
            ArrayList<Integer> list = new ArrayList<>();
            int left,right,mid,size,last,target,pos;
            // 双指针
            for(int i=0; i<n; i++){
                for(int j=i+1; j<n; j++){
                    target = Math.abs(nums.get(i)-nums.get(j));
                    size = list.size();
                    if(size == 0){
                        list.add(target);
                        continue;
                    }
                    last = list.get(size-1);
                    // 直接附加
                    if(last <= target){
                        pos = size;
                        if(pos+1 <= k){
                            list.add(pos, target);
                        }
                    }
                    // 二分查找
                    else{
                        left = 0;
                        right = size-1;
                        while(left <= right){
                            mid = (left+right)>>1;
                            if(list.get(mid) <= target){
                                left = mid+1;
                            }else if(list.get(mid) > target){
                                right = mid-1;
                            }
                        }
    
                        pos = left;
                        if(pos+1 <= k){
                            list.add(pos, target);
                        }
                    }
                }
            }
    
            return list.get(k-1);
        }
    
        /**
         * 排序 + 二分 + 双指针
         * @param nums
         * @param k
         * @return
         */
        private int solution3(ArrayList<Integer> nums, int k){
            // 先排序 更有利
            Collections.sort(nums);
    
            int n = nums.size();
            int left = 0;
            int right = nums.get(n-1)-nums.get(0);
            int mid;
            // 二分
            while(left <= right){
                mid = left+(right-left)/2;
                // left最终指向第一个cnt大于等于k的数
                // if(check(nums, k, mid)){
                if(check1(nums, k, mid)){
                    left = mid+1;
                }else{
                    right = mid-1;
                }
            }
    
            return left;
        }
    
        /**
         * 校验: 小于等于mid的个数(cnt)是否小于k
         * @param nums
         * @param k
         * @param mid
         * @return
         */
        private boolean check(ArrayList<Integer> nums, int k, int mid){
            int n = nums.size();
            // 小于等于mid的个数
            int cnt = 0;
            // 双指针
            for(int i=0; i<n; i++){
                int j;
                for(j=i+1; j<n; j++){
                    if(nums.get(j)-nums.get(i) > mid){
                        break;
                    }
                }
                cnt += j-i-1;
                if(cnt >= k){
                    return false;
                }
            }
    
            return true;
        }
    
        /**
         * 校验: 小于等于mid的个数(cnt)是否小于k
         * 
         * 再次二分 进行优化
         * 
         * @param nums
         * @param k
         * @param target
         * @return
         */
        private boolean check1(ArrayList<Integer> nums, int k, int target){
            int n = nums.size();
            // 小于等于target的个数
            int cnt = 0;
            // 双指针
            for(int i=0; i<n; i++){
                // 再次二分 进行优化
                int left=i+1,right=n-1;
                int mid;
                while(left <= right){
                    mid = left+((right-left)>>1);
                    // left最终指向第一个满足条件(nums.get(left)-nums.get(i) > target)的位置(从左往右)
                    if(nums.get(mid)-nums.get(i) <= target){
                        left = mid+1;
                    }else{
                        right = mid-1;
                    }
                }
                cnt += left-i-1;
                if(cnt >= k){
                    return false;
                }
            }
    
            return true;
        }
    }

  

