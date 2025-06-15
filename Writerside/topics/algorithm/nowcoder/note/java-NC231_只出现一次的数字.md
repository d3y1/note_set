# java-NC231 只出现一次的数字


    import java.util.*;
    
    /**
     * NC231 只出现一次的数字
     * @author d3y1
     */
    public class Solution {
        // T -> Times 出现次数
        private final int T = 2;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC227 只出现一次的数字(二) [nowcoder]
         *
         * @param nums int整型一维数组
         * @return int整型
         */
        public int singleNumber (int[] nums) {
            // return solution1(nums);
            return solution2(nums);
            // return solution22(nums);
            // return solution3(nums);
            // return solution4(nums);
        }
    
        /**
         * 位运算: 异或
         * @param nums
         * @return
         */
        private int solution1(int[] nums){
            int xorsum = 0;
            for(int num: nums){
                xorsum ^= num;
            }
    
            return xorsum;
        }
    
        /**
         * 位运算: 数位累加求余
         * @param nums
         * @return
         */
        private int solution2(int[] nums){
            // 比特位数
            int len = 32;
            // 同位比特累加
            int[] bitSum = new int[len];
            for(int num: nums){
                for(int i=0; i<len; i++){
                    bitSum[i] += ((num>>i)&1);
                }
            }
    
            int result = 0;
            for(int i=31; i>=0; i--){
                // bitSum[i]%T -> 消去出现T次的数的数位,剩余出现一次的数的数位
                result = (result<<1)+(bitSum[i]%T);
            }
    
            return result;
        }
    
        /**
         * 位运算: 数位累加求余
         * @param nums
         * @return
         */
        private int solution22(int[] nums){
            // 比特位数
            int len = 32;
            // 同位比特累加
            int[] bitSum = new int[len];
            for(int num: nums){
                for(int i=0; i<len; i++){
                    bitSum[i] += ((num>>i)&1);
                }
            }
    
            int result = 0;
            for(int i=31; i>=0; i--){
                // bitSum[i]%T -> 消去出现T次的数的数位,剩余出现一次的数的数位
                if(bitSum[i]%T == 1){
                    result |= (1<<i);
                }
            }
    
            return result;
        }
    
        /**
         * 哈希: HashMap
         * @param nums
         * @return
         */
        private int solution3(int[] nums){
            HashMap<Integer,Integer> map = new HashMap<>();
            for(int num: nums){
                map.put(num, map.getOrDefault(num,0)+1);
                if(map.get(num) == T){
                    map.remove(num);
                }
            }
    
            Integer[] result = map.keySet().toArray(new Integer[0]);
    
            return result[0];
        }
    
        /**
         * 哈希: HashSet
         * @param nums
         * @return
         */
        private int solution4(int[] nums){
            HashSet<Integer> set = new HashSet<>();
            for(int num: nums){
                if(set.contains(num)){
                    set.remove(num);
                }else{
                    set.add(num);
                }
            }
    
            Integer[] result = set.toArray(new Integer[set.size()]);
            // Integer[] result = set.stream().toArray(Integer[]::new);
    
            return result[0];
        }
    }

  

