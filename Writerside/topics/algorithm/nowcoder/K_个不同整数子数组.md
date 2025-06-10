# K 个不同整数子数组
https://www.nowcoder.com/practice/ac380725961a46a2b0747f803f96d6e7

    import java.util.*;
    
    /**
     * NC401 K 个不同整数子数组
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC343 和大于等于K的最短子数组     [nowcoder]
         * 相似 -> NC41 最长无重复子数组            [nowcoder]
         * 相似 -> NC170 最长不含重复字符的子字符串   [nowcoder]
         * 相似 -> NC356 至多包含K种字符的子串       [nowcoder]
         * 相似 -> NC387 找到字符串中的异位词        [nowcoder]
         *
         * @param nums int整型ArrayList
         * @param k int整型
         * @return int整型
         */
        public int nowsubarray (ArrayList<Integer> nums, int k) {
            // return solution1(nums, k);
            return solution2(nums, k);
            // return solution3(nums, k);
        }
    
        /**
         * 双指针
         * 
         * 恰好存在K个不同整数的连续子数组的个数 = 最多存在K个不同整数的连续子数组的个数 - 最多存在K−1个不同整数的连续子数组的个数
         * 
         * @param nums
         * @param k
         * @return
         */
        private int solution1(ArrayList<Integer> nums, int k){
            return atMostKDistinctKinds(nums, k)-atMostKDistinctKinds(nums, k-1);
        }
    
        /**
         * 获取连续子数组个数: 最多存在K个不同整数
         * @param nums
         * @param k
         * @return
         */
        private int atMostKDistinctKinds(ArrayList<Integer> nums, int k){
            int n = nums.size();
            // 统计滑动窗口中不同整数的个数
            int[] cnt = new int[n+1];
    
            int result = 0;
    
            // 双指针 毛毛虫
            int left = 0;
            int right = 0;
            // 滑动窗口[left, right)中整数种数
            int kind = 0;
            int numL,numR;
            while(right < n){
                numR = nums.get(right);
                if(cnt[numR] == 0){
                    kind++;
                }
                cnt[numR]++;
                right++;
    
                while(kind > k){
                    numL = nums.get(left);
                    cnt[numL]--;
                    if(cnt[numL] == 0){
                        kind--;
                    }
                    left++;
                }
    
                // 以nums[right-1]为右边界(固定nums[right-1]) 向左统计最多存在K个不同整数的连续子数组的个数
                result += right-left;
            }
    
            return result;
        }
    
        /**
         * 双指针
         * 
         * 恰好存在K个不同整数的连续子数组的个数 = 最多存在K个不同整数的连续子数组的个数 - 最多存在K−1个不同整数的连续子数组的个数
         * 
         * 简化
         * 
         * @param nums
         * @param k
         * @return
         */
        private int solution2(ArrayList<Integer> nums, int k){
            return getSubsAtMostKDistinctKinds(nums, k)-getSubsAtMostKDistinctKinds(nums, k-1);
        }
    
        /**
         * 获取连续子数组个数: 最多存在K个不同整数
         * @param nums
         * @param k
         * @return
         */
        private int getSubsAtMostKDistinctKinds(ArrayList<Integer> nums, int k){
            int n = nums.size();
            // 统计滑动窗口中不同整数的个数
            int[] cnt = new int[n+1];
    
            int result = 0;
    
            // 双指针 毛毛虫
            int left=0,right=0;
            // 滑动窗口[left, right)中整数种数
            int kind = 0;
            int numL,numR;
            while(right < n){
                numR = nums.get(right++);
                if(cnt[numR]++ == 0){
                    kind++;
                }
    
                while(kind > k){
                    numL = nums.get(left++);
                    cnt[numL]--;
                    if(cnt[numL] == 0){
                        kind--;
                    }
                }
    
                // 以nums[right-1]为右边界(固定nums[right-1]) 向左统计最多存在K个不同整数的连续子数组的个数
                result += right-left;
            }
    
            return result;
        }
    
        /**
         * 双指针
         * 
         * 恰好存在K个不同整数的连续子数组的个数 = 最多存在K个不同整数的连续子数组的个数 - 最多存在K−1个不同整数的连续子数组的个数
         * 
         * 合并
         * 
         * @param nums
         * @param k
         * @return
         */
        private int solution3(ArrayList<Integer> nums, int k){
            int n = nums.size();
            // 统计滑动窗口中不同整数的个数
            int[] cnt1 = new int[n+1];
            int[] cnt2 = new int[n+1];
    
            int result = 0;
    
            // 双指针 毛毛虫
            int left1=0,left2=0,right=0;
            // 滑动窗口[left1, right)和[left2, right)中整数种数
            int kind1=0,kind2=0;
            int numL1,numL2,numR;
            while(right < n){
                numR = nums.get(right++);
                if(cnt1[numR]++ == 0){
                    kind1++;
                }
                if(cnt2[numR]++ == 0){
                    kind2++;
                }
    
                while(kind1 > k){
                    numL1 = nums.get(left1++);
                    cnt1[numL1]--;
                    if(cnt1[numL1] == 0){
                        kind1--;
                    }
                }
    
                while(kind2 > k-1){
                    numL2 = nums.get(left2++);
                    cnt2[numL2]--;
                    if(cnt2[numL2] == 0){
                        kind2--;
                    }
                }
    
                // 以nums[right-1]为右边界(固定nums[right-1]) 向左统计 最多存在K个不同整数的连续子数组的个数与最多存在K-1个不同整数的连续子数组的个数之差
                // (right-left1)-(right-left2) = left2-left1
                result += left2-left1;
            }
    
            return result;
        }
    }
    

