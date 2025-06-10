# 和大于等于K的最短子数组
https://www.nowcoder.com/practice/3e1fd3d19fb0479d94652d49c7e1ead1

    import java.util.*;
    
    /**
     * NC343 和大于等于K的最短子数组
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型ArrayList
         * @param k int整型
         * @return int整型
         */
        public int shortestSubarray (ArrayList<Integer> nums, int k) {
            // return solution1(nums, k);
            // return solution2(nums, k);
            return solution3(nums, k);
        }
    
        /**
         * 二分
         * @param nums 正整数数组!
         * @param k
         * @return
         */
        private int solution1(ArrayList<Integer> nums, int k){
            int n = nums.size();
    
            // 前缀和
            long[] preSum = new long[n+1];
            for(int i=1; i<=n; i++){
                preSum[i] = preSum[i-1]+nums.get(i-1);
            }
    
            int result = Integer.MAX_VALUE;
            int left = 1;
            int right = n;
            int mid;
            // 二分
            while(left <= right){
                mid = left+(right-left)/2;
                if(check(preSum, k, mid)){
                    result = Math.min(result, mid);
                    right = mid-1;
                }else{
                    left = mid+1;
                }
            }
    
            return result==Integer.MAX_VALUE?-1:result;
        }
    
        /**
         * 校验gap大小窗口是否满足条件(preSum[j]-preSum[i] >= k)
         * @param preSum
         * @param target
         * @param gap
         * @return
         */
        private boolean check(long[] preSum, int target, int gap){
            for(int i=0,j=i+gap; j<preSum.length; i++,j++){
                if(preSum[j]-preSum[i] >= target){
                    return true;
                }
            }
    
            return false;
        }
    
        /**
         * 双指针: 滑动窗口
         * @param nums 正整数数组!
         * @param k
         * @return
         */
        private int solution2(ArrayList<Integer> nums, int k){
            int n = nums.size();
            int result = Integer.MAX_VALUE;
    
            int left=0;
            int right=0;
            int sum = 0;
            int numL,numR;
            while(right < n){
                numR = nums.get(right++);
                if(numR >= k){
                    return 1;
                }
    
                sum += numR;
                while(left<=right && sum>=k){
                    result = Math.min(result, right-left);
                    numL = nums.get(left++);
                    sum -= numL;
                }
            }
    
            return result==Integer.MAX_VALUE?-1:result;
        }
    
        /**
         * 单调栈: 单调增
         * @param nums 整数数组!
         * @param k
         * @return
         */
        private int solution3(ArrayList<Integer> nums, int k){
            int n = nums.size();
    
            // 前缀和
            long[] preSum = new long[n+1];
            for(int i=1; i<=n; i++){
                preSum[i] = preSum[i-1]+nums.get(i-1);
            }
    
            int result = Integer.MAX_VALUE;
    
            Deque<Integer> queue = new ArrayDeque<>();
            for(int i=0; i<=n; i++){
                long curSum = preSum[i];
                // 判断 是否满足条件(>=k)
                while(!queue.isEmpty() && curSum-preSum[queue.peekFirst()]>=k){
                    result = Math.min(result, i-queue.pollFirst());
                }
                // 单调栈(单调增)
                while(!queue.isEmpty() && preSum[queue.peekLast()]>=curSum){
                    queue.pollLast();
                }
                queue.offerLast(i);
            }
    
            return result==Integer.MAX_VALUE?-1:result;
        }
    }
    

