# java-NC321 连续数组的长度


    import java.util.*;
    
    /**
     * NC321 连续数组的长度
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
        public int findMaxLength (ArrayList<Integer> nums) {
             return solution(nums);
        }
    
        /**
         * 前缀和 + 哈希
         * @param nums
         * @return
         */
        private int solution(ArrayList<Integer> nums){
            int n = nums.size();
    
            HashMap<Integer, Integer> map = new HashMap<>();
            map.put(0, -1);
    
            int len = 0;
            int counter = 0;
            int num;
            for(int i=0; i<n; i++){
                num = nums.get(i);
                if(num == 0){
                    counter--;
                }else{
                    counter++;
                }
                if(map.containsKey(counter)){
                    int preIndex = map.get(counter);
                    len = Math.max(len, i-preIndex);
                }else{
                    map.put(counter, i);
                }
            }
    
            return len;
        }
    }

  

