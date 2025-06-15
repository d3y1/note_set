# java-NC308 过河


    import java.util.*;
    
    /**
     * NC308 过河
     * @author d3y1
     */
    public class Solution {
        // t*(t-1)
        private int PERIOD;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param l int整型
         * @param s int整型
         * @param t int整型
         * @param nums int整型ArrayList
         * @return int整型
         */
        public int crossRiver (int l, int s, int t, ArrayList<Integer> nums) {
            return solution1(l, s, t, nums);
            // return solution2(l, s, t, nums);
            // return solution3(l, s, t, nums);
        }
    
        /**
         * 动态规划 + 数学法(离散化)
         *
         * dp[i]表示跳到位置i处最少需要踩到的石子数
         *
         *         { Math.min(dp[i], dp[i-j]+1)  , stoneSet.contains(i)  && s<=j<=t
         * dp[i] = {
         *         { Math.min(dp[i], dp[i-j])    , !stoneSet.contains(i) && s<=j<=t
         *
         * @param l
         * @param s
         * @param t
         * @param nums
         * @return
         */
        private int solution1(int l, int s, int t, ArrayList<Integer> nums){
            if(l <= t){
                return 0;
            }
    
            int result = 0;
    
            // 1 只能跳跃一种距离
            if(s == t){
                for(int stone: nums){
                    if(stone%t==0 && stone<=l){
                        result++;
                    }
                }
    
                return result;
            }
    
            // 2 可以跳跃多种距离
            // 离散化处理 <- l很大 m很小
            PERIOD = t * (t-1);
            Collections.sort(nums);
            int m = nums.size();
            int[] stones = new int[m];
            int distance;
            HashSet<Integer> stoneSet = new HashSet<>();
            for(int i=0; i<m; i++){
                if(i == 0){
                    distance = nums.get(i);
                    stones[i] = distance % PERIOD;
                }else{
                    distance = nums.get(i)- nums.get(i-1);
                    stones[i] = stones[i-1] + distance % PERIOD;
                }
                stoneSet.add(stones[i]);
            }
            distance = l - stones[m-1];
            l = stones[m-1] + distance % PERIOD;
    
            int[] dp = new int[l+t];
            Arrays.fill(dp, Integer.MAX_VALUE>>1);
    
            // init
            for(int i=s; i<=t; i++){
                if(stoneSet.contains(i)){
                    dp[i] = 1;
                }else{
                    dp[i] = 0;
                }
            }
    
            for(int i=t+1; i<l+t; i++){
                for(int j=s; j<=t; j++){
                    if(dp[i-j] != Integer.MAX_VALUE>>1){
                        if(stoneSet.contains(i)){
                            dp[i] = Math.min(dp[i], dp[i-j]+1);
                        }else{
                            dp[i] = Math.min(dp[i], dp[i-j]);
                        }
                    }
                }
            }
    
            result = Integer.MAX_VALUE;
            for(int i=l; i<l+t; i++){
                result = Math.min(result, dp[i]);
            }
    
            return result;
        }
    
        /**
         * 动态规划: OOM
         *
         * dp[i]表示跳到位置i处最少需要踩到的石子数
         * 
         *         { Math.min(dp[i], dp[i-j]+1)  , stoneSet.contains(i)  && s<=j<=t
         * dp[i] = {
         *         { Math.min(dp[i], dp[i-j])    , !stoneSet.contains(i) && s<=j<=t
         *
         * @param l
         * @param s
         * @param t
         * @param nums
         * @return
         */
        private int solution2(int l, int s, int t, ArrayList<Integer> nums){
            if(l <= t){
                return 0;
            }
    
            int result = 0;
    
            // 1 只能跳跃一种距离
            if(s == t){
                for(int stone: nums){
                    if(stone%t==0 && stone<=l){
                        result++;
                    }
                }
    
                return result;
            }
    
            // 2 可以跳跃多种距离
            HashSet<Integer> stoneSet = new HashSet<>();
            for(int num: nums){
                stoneSet.add(num);
            }
    
            // 此处所需内存过大
            int[] dp = new int[l+t];
            Arrays.fill(dp, Integer.MAX_VALUE>>1);
    
            // init
            for(int i=s; i<=t; i++){
                if(stoneSet.contains(i)){
                    dp[i] = 1;
                }else{
                    dp[i] = 0;
                }
            }
    
            for(int i=t+1; i<l+t; i++){
                for(int j=s; j<=t; j++){
                    if(dp[i-j] != Integer.MAX_VALUE>>1){
                        if(stoneSet.contains(i)){
                            dp[i] = Math.min(dp[i], dp[i-j]+1);
                        }else{
                            dp[i] = Math.min(dp[i], dp[i-j]);
                        }
                    }
                }
            }
    
            result = Integer.MAX_VALUE;
            for(int i=l; i<l+t; i++){
                result = Math.min(result, dp[i]);
            }
    
            return result;
        }
    
        /**
         * 动态规划: 超时
         *
         * dp[i]表示跳到位置i处最少需要踩到的石子数
         *
         *         { Math.min(dp[i], dp[i-j]+1)  , stoneSet.contains(i)  && s<=j<=t
         * dp[i] = {
         *         { Math.min(dp[i], dp[i-j])    , !stoneSet.contains(i) && s<=j<=t
         *
         * @param l
         * @param s
         * @param t
         * @param nums
         * @return
         */
        private int solution3(int l, int s, int t, ArrayList<Integer> nums){
            if(l <= t){
                return 0;
            }
    
            int result = 0;
    
            // 1 只能跳跃一种距离
            if(s == t){
                for(int stone: nums){
                    if(stone%t==0 && stone<=l){
                        result++;
                    }
                }
    
                return result;
            }
    
            // 2 可以跳跃多种距离
            HashSet<Integer> stoneSet = new HashSet<>();
            for(int num: nums){
                stoneSet.add(num);
            }
    
            int[] dp = new int[s+t];
            Arrays.fill(dp, Integer.MAX_VALUE>>1);
    
            // init
            for(int i=s; i<=t; i++){
                if(stoneSet.contains(i)){
                    dp[i] = 1;
                }else{
                    dp[i] = 0;
                }
            }
            for(int i=t+1; i<s+t; i++){
                for(int j=s; j<=t; j++){
                    if(dp[i-j] != Integer.MAX_VALUE>>1){
                        if(stoneSet.contains(i)){
                            dp[i] = Math.min(dp[i], dp[i-j]+1);
                        }else{
                            dp[i] = Math.min(dp[i], dp[i-j]);
                        }
                    }
                }
            }
    
            result = Integer.MAX_VALUE>>1;
            int len = t-s+1;
            // 使用队列似乎更佳
            for(int i=0; i<t; i++){
                dp[i] = dp[s+i];
            }
            // 此处循环耗时过多
            for(int i=s+t; i<l+t; i++){
                int curr = Integer.MAX_VALUE>>1;
                int start = (i-s)%t;
                int index;
                for(int j=0; j<len; j++){
                    index = (start+j)%t;
                    if(dp[index] != Integer.MAX_VALUE>>1){
                        curr = Math.min(curr, dp[index]);
                        if(stoneSet.contains(i)){
                            curr++;
                        }
                    }
                }
    
                dp[start] = curr;
    
                if(i >= l){
                    result = Math.min(result, curr);
                }
            }
    
            return result;
        }
    }

  

