# java-NC404 最接近的K个元素


    import java.util.*;
    
    /**
     * NC404 最接近的K个元素
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型ArrayList
         * @param k int整型
         * @param x int整型
         * @return int整型ArrayList
         */
        public ArrayList<Integer> closestElement (ArrayList<Integer> nums, int k, int x) {
            // return solution1(nums, k, x);
            return solution2(nums, k, x);
        }
    
        /**
         * 二分
         *
         * 适合k较小的情况
         *
         * @param nums
         * @param k
         * @param x
         * @return
         */
        private ArrayList<Integer> solution1(ArrayList<Integer> nums, int k, int x){
            int n = nums.size();
    
            // 二分
            int left = 0;
            int right = n-1;
            int mid;
            while(left <= right){
                mid = left+((right-left)>>1);
                // left最终指向nums中第一个大于等于x的位置
                if(nums.get(mid) < x){
                    left = mid+1;
                }else{
                    right = mid-1;
                }
            }
    
            // 结果集
            ArrayList<Integer> resultList = new ArrayList<>();
            int L = left-1;
            int R = left;
            while(k-- > 0){
                // 左边到头
                if(L < 0){
                    resultList.add(nums.get(R++));
                    continue;
                }
                // 右边到尾
                if(n-1 < R){
                    resultList.add(0, nums.get(L--));
                    continue;
                }
    
                // L<R => nums.get(L)<=nums.get(R)
                if(Math.abs(nums.get(L)-x) <= Math.abs(nums.get(R)-x)){
                    resultList.add(0, nums.get(L--));
                }else if(Math.abs(nums.get(L)-x) > Math.abs(nums.get(R)-x)){
                    resultList.add(nums.get(R++));
                }
            }
    
            return resultList;
        }
    
        /**
         * 双指针
         *
         * 适合k较大的情况
         *
         * @param nums
         * @param k
         * @param x
         * @return
         */
        private ArrayList<Integer> solution2(ArrayList<Integer> nums, int k, int x){
            int n = nums.size();
            int left = 0;
            int right = n-1;
            while(left+k <= right){
                if(Math.abs(nums.get(left)-x) > Math.abs(nums.get(right)-x)) {
                    left++;
                }else{
                    right--;
                }
            }
    
            return new ArrayList<>(nums.subList(left, left+k));
        }
    }

  

