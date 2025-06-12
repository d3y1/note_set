# 二分查找-II
https://www.nowcoder.com/practice/4f470d1d3b734f8aaf2afb014185b395

    import java.util.*;
    
    /**
     * NC105 二分查找-II
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 如果目标值存在返回下标，否则返回 -1
         * @param nums int整型一维数组 
         * @param target int整型 
         * @return int整型
         */
        public int search (int[] nums, int target) {
            return solution1(nums, target);
            // return solution2(nums, target);
            // return solution3(nums, target);
        }
    
        /**
         * 二分
         * @param nums
         * @param target
         * @return
         */
        private int solution1(int[] nums, int target){
            int result = -1;
    
            int n = nums.length;
            if(n == 0){
                return result;
            }
            
            int left = 0;
            int right = n-1;
            int mid;
            while(left <= right){
                mid = (left+right)/2;
                if(nums[mid] < target){
                    left = mid + 1;
                }else if(nums[mid] > target){
                    right = mid -1;
                }else{
                    result = mid;
                    right = mid - 1;
                }
            }
    
            return result;
        }
    
        /**
         * 二分
         * @param nums
         * @param target
         * @return
         */
        private int solution2(int[] nums, int target){
            int result = -1;
    
            int n = nums.length;
            if(n == 0){
                return result;
            }
    
            int left = 0;
            int right = n-1;
            int mid;
            while(left <= right){
                mid = (left+right)/2;
                if(nums[mid] < target){
                    left = mid + 1;
                }else{
                    right = mid - 1;
                }
            }
    
            return nums[left]==target ? left : -1;
        }
    
        /**
         * 二分
         * @param nums
         * @param target
         * @return
         */
        private int solution3(int[] nums, int target){
            int result = -1;
    
            int n = nums.length;
            if(n == 0){
                return result;
            }
    
            int left = 0;
            int right = n-1;
            int mid;
            while(left < right){
                mid = (left+right)/2;
                if(nums[mid] < target){
                    left = mid + 1;
                }else{
                    right = mid;
                }
            }
    
            return nums[left]==target ? left : -1;
        }
    }
    

