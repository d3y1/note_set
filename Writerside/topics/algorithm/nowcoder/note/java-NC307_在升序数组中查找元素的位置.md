# java-NC307 在升序数组中查找元素的位置


    import java.util.*;
    
    /**
     * NC307 在升序数组中查找元素的位置
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型ArrayList
         * @param target int整型
         * @return int整型ArrayList
         */
        public ArrayList<Integer> searchRange (ArrayList<Integer> nums, int target) {
            return solution(nums, target);
        }
    
        /**
         * 二分
         * @param nums
         * @param target
         * @return
         */
        private ArrayList<Integer> solution(ArrayList<Integer> nums, int target){
            int n = nums.size();
    
            ArrayList<Integer> result = new ArrayList<>();
    
            // down: target下界
            int down = -1;
            // 二分查找target下界
            int left = 0;
            int right = n-1;
            int mid;
            while(left <= right){
                mid = (left+right)>>1;
                if(nums.get(mid) < target){
                    left = mid+1;
                }else if(nums.get(mid) > target){
                    right = mid-1;
                }else{
                    down = mid;
                    right = mid-1;
                }
            }
    
            // target未找到
            if(down == -1){
                result.add(-1);
                result.add(-1);
                return result;
            }
    
            // up: target上界
            int up = -1;
            // 二分查找target上界(可从down开始)
            left = down;
            right = n-1;
            while(left <= right){
                mid = (left+right)>>1;
                if(nums.get(mid) < target){
                    left = mid+1;
                }else if(nums.get(mid) > target){
                    right = mid-1;
                }else{
                    up = mid;
                    left = mid+1;
                }
            }
    
            result.add(down);
            result.add(up);
    
            return result;
        }
    }

  

