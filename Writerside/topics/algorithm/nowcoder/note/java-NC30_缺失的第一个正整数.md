# java-NC30 缺失的第一个正整数


    import java.util.*;
    
    /**
     * NC30 缺失的第一个正整数
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型一维数组
         * @return int整型
         */
        public int minNumberDisappeared (int[] nums) {
            // return solution1(nums);
            return solution2(nums);
            // return solution3(nums);
        }
    
        /**
         * 哈希: TreeSet
         * 
         * 数组元素可重复
         *
         * @param nums
         * @return
         */
        private int solution1(int[] nums){
            TreeSet<Integer> treeSet = new TreeSet<>();
            for(int num: nums){
                if(num > 0){
                    treeSet.add(num);
                }
            }
    
            int min = 1;
            for(int num: treeSet){
                if(num > min){
                    return min;
                }
                min++;
            }
    
            return min;
        }
    
        /**
         * 原地哈希: 标记法
         *
         * 数组元素可重复
         *
         * 相似 -> NC305 寻找唯一重复数 [nowcoder]
         *
         * 对于一个长度为N的数组, 其中没有出现的最小正整数只能在[1,N+1]中.
         * 这是因为如果[1,N]都出现了, 那么答案是N+1, 否则答案是[1,N]中没有出现的最小正整数.
         * 这样一来, 我们将所有在[1,N]范围内的数放入哈希表, 可以得到最终的答案, 而给定的数组恰好长度为N.
         *
         * @param nums
         * @return
         */
        private int solution2(int[] nums){
            int n = nums.length;
            for(int i=0; i<n; i++){
                // 无效数置为n+1 不影响最终结果
                if(nums[i] <= 0){
                    nums[i] = n+1;
                }
            }
    
            int idx;
            for(int num: nums){
                num = Math.abs(num);
                // 1<=num<=n -> num为有效数
                if(num <= n){
                    // 0<=idx<=n-1
                    idx = num-1;
                    // 标记为负值 表示num=idx+1的数已存在 -> 有效数num标记转化为索引位置num-1
                    nums[idx] = -Math.abs(nums[idx]);
                }
            }
    
            // 依次判断
            for(int i=0; i<n; i++){
                // 表示num=i+1的数不存在
                if(nums[i] > 0){
                    return i+1;
                }
            }
    
            return n+1;
        }
    
        /**
         * 原地哈希: 置换法
         *
         * 数组元素可重复
         *
         * @param nums
         * @return
         */
        private int solution3(int[] nums){
            int n= nums.length;
            int num;
            for(int i=0; i<n; i++){
                num = nums[i];
                // 1<=num<=n -> num为有效数; 0<=num-1<=n-1, 有效数num置换到索引位置num-1
                while((1<=num&&num<=n) && num!=nums[num-1]){
                    swap(nums, i, num-1);
                    num = nums[i];
                }
            }
    
            // 依次判断
            for(int i=0; i<n; i++){
                // 表示num=i+1的数不存在
                if(nums[i] != i+1){
                    return i+1;
                }
            }
    
            return n+1;
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

  

