# java-NC385 划分等和序列


    import java.util.*;
    
    /**
     * NC385 划分等和序列
     * @author d3y1
     */
    public class Solution {
        private int avg;
        private int N;
    
        private boolean[] visited;
    
        private boolean[] memo;
    
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param nums int整型ArrayList
         * @param k int整型
         * @return bool布尔型
         */
        public boolean candivide (ArrayList<Integer> nums, int k) {
            // return solution1(nums, k);
            // return solution2(nums, k);
            return solution3(nums, k);
            // return solution4(nums, k);
        }
    
        /**
         * 动态规划: 01背包
         *
         * dp[j]表示背包大小为j时能够组成的最大的和(数组中的元素和)[数组中每个元素仅用一次]
         *
         * dp[j] = Math.max(dp[j], dp[j-num] + num)
         *
         * @param nums
         * @param k
         * @return
         */
        private boolean solution1(ArrayList<Integer> nums, int k){
            int n = nums.size();
    
            int sum = 0;
            for(int i=0; i<n; i++){
                sum += nums.get(i);
            }
    
            if(sum%k != 0){
                return false;
            }
            avg = sum/k;
    
            int[] dp = new int[sum+1];
            int num;
            for(int i=0; i<n; i++){
                num = nums.get(i);
                if(num > avg){
                    return false;
                }
                // 数组中每个元素仅用一次 -> 降序
                for(int j=sum; j>=num; j--){
                    dp[j] = Math.max(dp[j], dp[j-num] + num);
                }
            }
    
            // avg的倍数 均要判断
            for(int i=1; i<=k; i++){
                // 恰好装满 -> 恰好组成下一个元素和avg
                if(dp[avg*i] != avg*i){
                    return false;
                }
            }
    
            return true;
        }
    
        /**
         * dfs: 遍历解空间
         * @param nums
         * @param k
         * @return
         */
        private boolean solution2(ArrayList<Integer> nums, int k){
            int n = nums.size();
            visited = new boolean[n];
    
            int sum = 0;
            for(int i=0; i<n; i++){
                sum += nums.get(i);
            }
    
            if(sum%k != 0){
                return false;
            }
            int avg = sum/k;
    
            return dfs(nums, k, avg);
        }
    
        /**
         * dfs: 递归
         * @param nums
         * @param k
         * @param target
         * @return
         */
        private boolean dfs(ArrayList<Integer> nums, int k, int target){
            if(k == 0){
                return true;
            }
            if(target == 0){
                if(dfs(nums, k-1, avg)){
                    return true;
                }
            }else if(target < 0){
                return false;
            }else{
                for(int i=0; i<nums.size(); i++){
                    if(!visited[i]){
                        visited[i] = true;
                        if(dfs(nums, k, target-nums.get(i))){
                            return true;
                        }
                        visited[i] = false;
                    }
                }
            }
    
            return false;
        }
    
        /**
         * 状态压缩(位运算) + 记忆化搜索
         *
         * 给定长度为n的数组nums和整数k, 我们需要判断是否能将数组分成k个总和相等的非空子集.
         * 首先计算数组的和sum, 如果sum不是k的倍数, 那么不可能能有合法方案, 此时直接返回False.
         * 否则我们需要得到k个和为avg=sum/k的集合, 那么我们每次尝试选择一个还在数组中的数, 若选择后当前已选数字和等于avg则说明得到了一个集合,
         * 而已选数字和大于avg时, 不可能形成一个集合从而停止继续往下选择新的数字.
         *
         * 又因为n满足1≤n≤15, 所以我们可以用一个整数status来表示当前可用的数字集合: 从低位到高位, 第i位为1则表示数字nums[i]可以使用, 否则表示nums[i]已被使用.
         *
         * 为了避免相同状态的重复计算, 我们用memo[status]来表示在可用的数字状态为status的情况下是否可行, 初始全部状态为记录为可行状态True.
         * 这样我们就可以通过记忆化搜索这种「自顶向下」的方式来进行求解原始状态的可行性, 而当状态集合中不存在任何数字时, 即status=0时, 表示原始数组可以按照题目要求来进行分配, 此时返回True即可.
         *
         * @param nums
         * @param k
         * @return
         */
        private boolean solution3(ArrayList<Integer> nums, int k){
            N = nums.size();
    
            int sum = 0;
            for(int i=0; i<N; i++){
                sum += nums.get(i);
            }
    
            if(sum%k != 0){
                return false;
            }
            avg = sum/k;
    
            // 升序
            Collections.sort(nums);
            if(nums.get(N-1) > avg){
                return false;
            }
    
            // 记忆化搜索
            memo = new boolean[1<<N];
            Arrays.fill(memo, true);
            return dfs(nums, avg, (1<<N)-1, 0);
        }
    
        /**
         * 递归
         * @param nums
         * @param avg
         * @param status
         * @param remain
         * @return
         */
        private boolean dfs(ArrayList<Integer> nums, int avg, int status, int remain){
            if(status == 0){
                return true;
            }
    
            // 记忆化搜索
            if(!memo[status]){
                return false;
            }
            memo[status] = false;
    
            for(int i=0; i<N; i++){
                // nums事先排序 升序
                if(remain+nums.get(i) > avg){
                    break;
                }
                // nums[i]可选(即未被选择)
                if(((status>>i)&1) == 1){
                    // 选择nums[i] 且将nums[i]置为不可选 <- status^(1<<i)
                    if(dfs(nums, avg, status^(1<<i), (remain+nums.get(i))%avg)){
                        return true;
                    }
                }
            }
    
            return false;
        }
    
        /**
         * 状态压缩(位运算) + 动态规划
         *
         * 也可以用「动态规划」这种「自底向上」的方法来求解是否存在可行方案: 
         * 同样我们用一个整数status来表示当前可用的数字集合: 从低位到高位, 第i位为0则表示数字nums[i]可以使用, 否则表示nums[i]已被使用.
         * 
         * 然后我们用dp[status]来表示在可用的数字状态为status的情况下是否可能可行, 初始全部状态为记录为不可行状态False, 只记dp[0]=True为可行状态。
         * 
         * 同样我们每次对于当前状态下从可用的数字中选择一个数字, 若此时选择全部数字取模后小于等于avg, 则说明选择该数字后的状态再继续往下添加数字是可能满足题意的, 并且此时标记状为可能可行状态, 否则就一定不能达到满足.
         * 
         * 最终dp[U]即可, 其中U表示全部数字使用的集合状态(即status全1状态).
         *
         * @param nums
         * @param k
         * @return
         */
        private boolean solution4(ArrayList<Integer> nums, int k){
            N = nums.size();
    
            int sum = 0;
            for(int i=0; i<N; i++){
                sum += nums.get(i);
            }
    
            if(sum%k != 0){
                return false;
            }
            avg = sum/k;
    
            // 升序
            Collections.sort(nums);
            if(nums.get(N-1) > avg){
                return false;
            }
    
            // 动态规划
            boolean[] dp = new boolean[1<<N];
            int[] remain = new int[1<<N];
            dp[0] = true;
            int status;
            for(int i=0; i<(1<<N); i++){
                if(!dp[i]){
                    continue;
                }
                for(int j=0; j<N; j++){
                    if(remain[i]+nums.get(j) > avg){
                        break;
                    }
                    // nums[i]可选(即未被选择)
                    if(((i>>j)&1) == 0){
                        // 选择nums[i] 且将nums[i]置为不可选 <- i|(1<<j)
                        status = i|(1<<j);
                        if(!dp[status]){
                            remain[status] = (remain[i]+nums.get(j))%avg;
                            dp[status] = true;
                        }
                    }
                }
            }
    
            return dp[(1<<N)-1];
        }
    }

  

