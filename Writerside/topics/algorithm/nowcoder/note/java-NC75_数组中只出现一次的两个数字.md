# java-NC75 数组中只出现一次的两个数字


    import java.util.*;
    
    /**
     * NC75 数组中只出现一次的两个数字
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
        public int[] FindNumsAppearOnce (int[] nums) {
            // return solution1(nums);
            // return solution2(nums);
            return solution3(nums);
        }
    
        /**
         * 哈希: HashMap
         * @param nums
         * @return
         */
        private int[] solution1(int[] nums){
            HashMap<Integer,Integer> map = new HashMap<>();
            for(int num: nums){
                map.put(num, map.getOrDefault(num, 0)+1);
                if(map.get(num) == 2){
                    map.remove(num);
                }
            }
    
            int[] result = new int[map.size()];
            int i = 0;
            for(int key: map.keySet()){
                result[i++] = key;
            }
            Arrays.sort(result);
    
            return result;
        }
    
        /**
         * 哈希: HashSet
         * @param nums
         * @return
         */
        private int[] solution2(int[] nums){
            HashSet<Integer> set = new HashSet<>();
            for(int num: nums){
                if(set.contains(num)){
                    set.remove(num);
                }else{
                    set.add(num);
                }
            }
    
            int[] result = new int[set.size()];
            int i = 0;
            for(int key: set){
                result[i++] = key;
            }
            Arrays.sort(result);
    
            return result;
        }
    
        /**
         * 位运算
         *
         * lowBit 整数n在二进制表示下最低位1及后面的0所构成的数值
         * 参考树状数组(Binary Indexed Tree)(也称Fenwick树)
         * 参考 -> NC360 右侧更小数     [nowcoder]
         * 参考 -> NC349 计算数组的小和  [nowcoder]
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
         * lowBit(44) = n & (~n+1) = n & (-n) = 44 & (-44)
         *
         *
         * 
         * 假设数组 nums 中只出现一次的元素分别是 x1 和 x2
         * 如果把 nums 中的所有元素全部异或起来, 得到结果 xorsum, 那么一定有:
         * xorsum = x1 ^ x2
         *
         * 其中^表示异或运算, 这是因为 nums 中出现两次的元素都会因为异或运算的性质 a^b^b=a 抵消掉, 那么最终的结果就只剩下x1和x2的异或和(x1^x2)
         *
         * xorsum 显然不会等于0, 因为如果 xorsum=0, 那么说明x1=x2, 这样x1和x2就不是只出现一次的数字了(且xorsum=0时, lowBit=0&(-0)=0, 后续也无法分类)
         * 因此, 我们可以使用位运算 xorsum&-xorsum 取出 xorsum 的二进制表示中最低位那个1
         * 设其为第l位, 那么x1和x2中的某一个数的二进制表示的第l位为0, 且另一个数的二进制表示的第l位为1
         * 因为只有在这种情况下, x1^x2二进制表示的第l位才能为1
         *
         * 这样一来, 我们就可以把 nums 中的所有元素分成两类, 其中一类包含所有二进制表示的第l位为0的数, 另一类包含所有二进制表示的第l位为1的数
         * 可以发现:
         * 对于任意一个在数组 nums 中出现两次的元素, 该元素的两次出现都会被包含在同一类中;
         * 对于任意一个在数组 nums 中只出现了一次的元素, 即x1和x2, 它们会被包含在不同类中.
         *
         * 因此, 如果我们将每一类的元素全部异或起来, 那么其中一类会得到x1, 另一类会得到x2
         * 这样我们就找出了这两个只出现一次的元素.
         *
         * @param nums
         * @return
         */
        private int[] solution3(int[] nums){
            // 异或和
            int xorsum = 0;
            for(int num: nums){
                xorsum ^= num;
            }
    
            // 防溢出 8位有符 表示范围: 最大值01111111(127) 最小值10000000(-128)
            // xorsum = -128 => -xorsum = 128 -> 超出表示范围(溢出)
            int lowBit = (xorsum==Integer.MIN_VALUE) ? xorsum: xorsum&(-xorsum);
            // 两类
            int type1=0,type2=0;
            for(int num: nums){
                // 二进制表示的第l位为0的数
                if((num&lowBit) == 0){
                    type1 ^= num;
                }
                // 二进制表示的第l位为1的数
                else{
                    type2 ^= num;
                }
            }
    
            int[] result = new int[]{type1, type2};
            Arrays.sort(result);
    
            return result;
        }
    }

  

