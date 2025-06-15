# java-NC406 最长山脉


    import java.util.*;
    
    /**
     * NC406 最长山脉
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型ArrayList
         * @return int整型
         */
        public int longestmountain (ArrayList<Integer> nums) {
            return solution1(nums);
            // return solution2(nums);
        }
    
        /**
         * 贪心
         * @param nums
         * @return
         */
        private int solution1(ArrayList<Integer> nums){
            int n = nums.size();
            if(n < 3){
                return 0;
            }
    
            int result = 0;
    
            int left,right;
            // 贪心
            for(int i=1; i+1<n;){
                // 当前位置 非山顶
                if(nums.get(i-1)>=nums.get(i) || nums.get(i)<=nums.get(i+1)){
                    i++;
                    continue;
                }
    
                // 左边界
                for(left=i; left-1>=0; left--){
                    if(nums.get(left-1) >= nums.get(left)){
                        break;
                    }
                }
    
                // 右边界
                for(right=i; right+1<n; right++){
                    if(nums.get(right) <= nums.get(right+1)){
                        break;
                    }
                }
    
                result = Math.max(result, right-left+1);
                i = right;
            }
    
            return result;
        }
    
        /**
         * 贪心
         * @param nums
         * @return
         */
        private int solution2(ArrayList<Integer> nums){
            int n = nums.size();
            if(n < 3){
                return 0;
            }
    
            int result = 0;
    
            // left[i]:  i左侧连续递减的元素个数
            int[] left = new int[n];
            // right[i]: i右侧连续递减的元素个数
            int[] right = new int[n];
    
    
            for(int i=1; i<n; i++){
                if(nums.get(i-1) < nums.get(i)){
                    left[i] = left[i-1]+1;
                }
            }
            for(int i=n-2; i>=0; i--){
                if(nums.get(i) > nums.get(i+1)){
                    right[i] = right[i+1]+1;
                }
            }
    
            for(int i=0; i<n; i++){
                // 当前位置 山顶
                if(left[i]>0 && right[i]>0){
                    result = Math.max(result, left[i]+right[i]+1);
                }
            }
    
            return result;
        }
    }

  

