# java-NC275 和为S的两个数字


    import java.util.*;
    import java.util.ArrayList;
    
    /**
     * NC275 和为S的两个数字
     * @author d3y1
     */
    public class Solution {
        /**
         * 相似 -> NC247 最接近的三数之和 [nowcoder]
         * @param array
         * @param sum
         * @return
         */
        public ArrayList<Integer> FindNumbersWithSum(int[] array,int sum) {
            // return solution1(array, sum);
            return solution2(array, sum);
            // return solution3(array, sum);
            // return solution4(array, sum);
        }
    
        /**
         * 暴力法
         * @param array
         * @param sum
         * @return
         */
        private ArrayList<Integer> solution1(int[] array, int sum){
            int len = array.length;
            ArrayList<Integer> list = new ArrayList<>();
    
            for(int i=0; i<len; i++){
                for(int j=i+1; j<len; j++){
                    if(array[i]+array[j] == sum){
                        list.add(array[i]);
                        list.add(array[j]);
                        return list;
                    }
                }
            }
    
            return list;
        }
    
        /**
         * 双指针: 对撞指针
         * @param array
         * @param sum
         * @return
         */
        private ArrayList<Integer> solution2(int[] array, int sum){
            int len = array.length;
            ArrayList<Integer> list = new ArrayList<>();
    
            int left = 0;
            int right = len-1;
            int val;
            while(left < right){
                val = array[left]+array[right];
                if(val < sum){
                    left++;
                }else if(val > sum){
                    right--;
                }else{
                    list.add(array[left]);
                    list.add(array[right]);
                    break;
                }
            }
    
            return list;
        }
    
        /**
         * 哈希
         * @param array
         * @param sum
         * @return
         */
        private ArrayList<Integer> solution3(int[] array, int sum){
            int len = array.length;
            ArrayList<Integer> list = new ArrayList<>();
    
            HashSet<Integer> set = new HashSet<>();
            int target;
            for(int i=0; i<len; i++){
                target = sum-array[i];
                if(set.contains(target)){
                    list.add(target);
                    list.add(array[i]);
                    break;
                }else{
                    set.add(array[i]);
                }
            }
    
            return list;
        }
    
        /**
         * 二分
         * @param array
         * @param sum
         * @return
         */
        private ArrayList<Integer> solution4(int[] array, int sum){
            int len = array.length;
            ArrayList<Integer> list = new ArrayList<>();
    
            int left,right,mid,target;
            for(int i=0; i<len; i++){
                if(array[i]*2 > sum){
                    break;
                }
                target = sum-array[i];
                left = i+1;
                right = len-1;
                while(left <= right){
                    mid = left+((right-left)>>1);
                    if(array[mid] < target){
                        left = mid+1;
                    }else if(array[mid] > target){
                        right = mid-1;
                    }else{
                        list.add(array[i]);
                        list.add(target);
                        return list;
                    }
                }
            }
    
            return list;
        }
    }

  

