# java-NC194 下一个排列


    import java.util.*;
    
    /**
     * NC194 下一个排列
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型一维数组
         * @return int整型一维数组
         */
        public int[] nextPermutation (int[] nums) {
            // return solution1(nums);
            // return solution11(nums);
            // return solution2(nums);
            return solution22(nums);
        }
    
        /**
         * 双指针
         * @param nums
         * @return
         */
        private int[] solution1(int[] nums){
            int n = nums.length;
            // 右边大于nums[i]的最小值
            int min = Integer.MAX_VALUE;
            // 右边大于nums[i]的最小值索引位置
            int idx = -1;
            // 双指针
            for(int i=n-2; i>=0; i--){
                for(int j=i+1; j<n; j++){
                    if(nums[i] < nums[j]){
                        if(nums[j] < min){
                            min = nums[j];
                            idx = j;
                        }
                    }
                }
                if(idx != -1){
                    swap(nums, i, idx);
                    // [from,to): [i+1,n)
                    Arrays.sort(nums, i+1, n);
                    return nums;
                }
            }
    
            // [from,to): [0,n)
            Arrays.sort(nums, 0, n);
    
            return nums;
        }
    
        /**
         * 二分
         * @param nums
         * @return
         */
        private int[] solution11(int[] nums){
            int n = nums.length;
            int left,right,mid,target;
            for(int i=n-2; i>=0; i--){
                // [from,to): [i+1,n)
                Arrays.sort(nums, i+1, n);
                left = i+1;
                right = n-1;
                target = nums[i];
                // 二分
                while(left <= right){
                    mid = left+((right-left)>>1);
                    // left最终指向第一个大于target的数(从左往右)
                    if(nums[mid] <= target){
                        left = mid+1;
                    }else{
                        right = mid-1;
                    }
                }
                if(left < n){
                    swap(nums, i, left);
                    return nums;
                }
            }
    
            // [from,to): [0,n)
            Arrays.sort(nums, 0, n);
    
            return nums;
        }
    
        /**
         * 双指针
         * @param nums
         * @return
         */
        private int[] solution2(int[] nums){
            int n = nums.length;
            int i = n-2;
            // 找到待交换位置
            while(i>=0 && nums[i]>=nums[i+1]){
                i--;
            }
            
            // 双指针
            if(i >= 0){
                int j = n-1;
                // i右边已经降序 找到第一个大于nums[i]的数(从右向左)
                while(j>=0 && nums[i]>=nums[j]){
                    j--;
                }
                swap(nums, i, j);
            }
            reverse(nums, i+1, n-1);
    
            return nums;
        }
    
        /**
         * 二分
         * @param nums
         * @return
         */
        private int[] solution22(int[] nums){
            int n = nums.length;
            int i = n-2;
            // 找到待交换位置
            while(i>=0 && nums[i]>=nums[i+1]){
                i--;
            }
            
            if(i >= 0){
                int left = i+1;
                int right = n-1;
                int mid;
                int target = nums[i];
                // 二分 i右边已经降序
                while(left <= right){
                    mid = left+((right-left)>>1);
                    // right最终指向第一个大于target的数(从右向左)
                    if(nums[mid] <= target){
                        right = right-1;
                    }else{
                        left = left+1;
                    }
                }
                swap(nums, i, right);
            }
            
            reverse(nums, i+1, n-1);
    
            return nums;
        }
    
        /**
         * 区间反转
         * @param nums
         * @param i
         * @param j
         */
        private void reverse(int[] nums, int i, int j){
            while(i < j){
                swap(nums, i++, j--);
            }
        }
    
        /**
         * 交换
         * @param nums
         * @param i
         * @param j
         */
        private void swap(int[] nums, int i, int j){
            int tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
        }
    }

  

