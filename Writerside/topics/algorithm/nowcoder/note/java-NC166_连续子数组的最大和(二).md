# java-NC166 连续子数组的最大和(二)


    import java.util.*;
    
    /**
     * NC166 连续子数组的最大和(二)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param array int整型一维数组
         * @return int整型一维数组
         */
        public int[] FindGreatestSumOfSubArray (int[] array) {
            // return solution1(array);
            // return solution11(array);
            // return solution2(array);
            // return solution22(array);
            // return solution3(array);
            return solution33(array);
        }
    
        /**
         * 动态规划 + 贪心
         *
         * len[i]表示以array[i]为结尾(必选)的连续子数组的长度
         * dp[i]表示以array[i]为结尾(必选)的连续子数组的最大和
         *
         *         { dp[i-1] + array[i]  , dp[i-1] >= 0
         * dp[i] = {
         *         { array[i]            , dp[i-1] < 0
         *
         *          { len[i-1] + 1  , dp[i-1] >= 0
         * len[i] = {
         *          { 1             , dp[i-1] < 0
         *
         * @param array
         * @return
         */
        private int[] solution1(int[] array){
            int n = array.length;
    
            int[] dp = new int[n];
            int[] len = new int[n];
    
            dp[0] = array[0];
            len[0] = 1;
    
            // 连续子数组的最大和
            int sum = dp[0];
            // 连续子数组(最大和)的最长长度
            int length = len[0];
            // 最长连续子数组(最大和)的最后位置
            int index = 0;
            for(int i=1; i<n; i++){
                // 贪心
                if(dp[i-1] >= 0){
                    dp[i] = dp[i-1]+array[i];
                    len[i] = len[i-1]+1;
                }else{
                    dp[i] = array[i];
                    len[i] = 1;
                }
                if(dp[i] > sum){
                    sum = dp[i];
                    length = len[i];
                    index = i;
                }
                if(dp[i] == sum){
                    if(len[i] > length){
                        length = len[i];
                        index = i;
                    }
                }
            }
    
            int[] result = new int[length];
            for(int i=index-length+1,j=0; i<=index; i++){
                result[j++] = array[i];
            }
    
            return result;
        }
    
        /**
         * 动态规划 + 贪心
         *
         * len[i]表示以数组中第i个整数为结尾(必选)的连续子数组的长度
         * dp[i]表示以数组中第i个整数为结尾(必选)的连续子数组的最大和
         *
         *         { dp[i-1] + array[i-1]  , dp[i-1] >= 0
         * dp[i] = {
         *         { array[i-1]            , dp[i-1] < 0
         *
         *          { len[i-1] + 1  , dp[i-1] >= 0
         * len[i] = {
         *          { 1             , dp[i-1] < 0
         *
         * @param array
         * @return
         */
        private int[] solution11(int[] array){
            int n = array.length;
    
            int[] dp = new int[n+1];
            int[] len = new int[n+1];
    
            dp[0] = Integer.MIN_VALUE;
            len[0] = 0;
    
            // 连续子数组的最大和
            int sum = Integer.MIN_VALUE;
            // 连续子数组(最大和)的最长长度
            int length = 0;
            // 最长连续子数组(最大和)的最后位置
            int index = 0;
            for(int i=1; i<=n; i++){
                // 贪心
                if(dp[i-1] >= 0){
                    dp[i] = dp[i-1]+array[i-1];
                    len[i] = len[i-1]+1;
                }else{
                    dp[i] = array[i-1];
                    len[i] = 1;
                }
                if(dp[i] > sum){
                    sum = dp[i];
                    length = len[i];
                    index = i;
                }
                if(dp[i] == sum){
                    if(len[i] > length){
                        length = len[i];
                        index = i;
                    }
                }
            }
    
            int[] result = new int[length];
            for(int i=index-length,j=0; i<index; i++){
                result[j++] = array[i];
            }
    
            return result;
        }
    
    
        /**
         * 动态规划(空间优化) + 贪心
         *
         * preLen 表示以数组中上一整数为结尾的连续子数组的长度
         * preSum 表示以数组中上一整数为结尾的连续子数组的最大和
         * curLen 表示以数组中当前整数为结尾的连续子数组的长度
         * curSum 表示以数组中当前整数为结尾的连续子数组的最大和
         *
         *          { preSum + array[i]  , preSum >= 0
         * curSum = {
         *          { array[i]           , preSum < 0
         *
         *          { preLen + 1  , preSum >= 0
         * curLen = {
         *          { 1           , preSum < 0
         *
         * @param array
         * @return
         */
        private int[] solution2(int[] array){
            int n = array.length;
    
            int curSum;
            int preSum = array[0];
            int curLen;
            int preLen = 1;
    
            // 连续子数组的最大和
            int sum = array[0];
            // 连续子数组(最大和)的最长长度
            int length = 1;
            // 最长连续子数组(最大和)的最后位置
            int index = 0;
            for(int i=1; i<n; i++){
                // 贪心
                if(preSum >= 0){
                    curSum = preSum+array[i];
                    curLen = preLen+1;
                }else{
                    curSum = array[i];
                    curLen = 1;
                }
                if(curSum > sum){
                    sum = curSum;
                    length = curLen;
                    index = i;
                }
                if(curSum == sum){
                    if(curLen > length){
                        length = curLen;
                        index = i;
                    }
                }
    
                preSum = curSum;
                preLen = curLen;
            }
    
            int[] result = new int[length];
            for(int i=index-length+1,j=0; i<=index; i++){
                result[j++] = array[i];
            }
    
            return result;
        }
    
        /**
         * 动态规划(空间优化) + 贪心
         *
         * preLen 表示以数组中上一整数为结尾的连续子数组的长度
         * preSum 表示以数组中上一整数为结尾的连续子数组的最大和
         * curLen 表示以数组中当前整数为结尾的连续子数组的长度
         * curSum 表示以数组中当前整数为结尾的连续子数组的最大和
         *
         *          { preSum + array[i-1]  , preSum >= 0
         * curSum = {
         *          { array[i-1]           , preSum < 0
         *
         *          { preLen + 1  , preSum >= 0
         * curLen = {
         *          { 1           , preSum < 0
         *
         * @param array
         * @return
         */
        private int[] solution22(int[] array){
            int n = array.length;
    
            int curSum;
            int preSum = Integer.MIN_VALUE;
            int curLen;
            int preLen = 0;
    
            // 连续子数组的最大和
            int sum = Integer.MIN_VALUE;
            // 连续子数组(最大和)的最长长度
            int length = 0;
            // 最长连续子数组(最大和)的最后位置
            int index = 0;
            for(int i=1; i<=n; i++){
                // 贪心
                if(preSum >= 0){
                    curSum = preSum+array[i-1];
                    curLen = preLen+1;
                }else{
                    curSum = array[i-1];
                    curLen = 1;
                }
                if(curSum > sum){
                    sum = curSum;
                    length = curLen;
                    index = i;
                }
                if(curSum == sum){
                    if(curLen > length){
                        length = curLen;
                        index = i;
                    }
                }
    
                preSum = curSum;
                preLen = curLen;
            }
    
            int[] result = new int[length];
            for(int i=index-length,j=0; i<index; i++){
                result[j++] = array[i];
            }
    
            return result;
        }
    
        /**
         * 动态规划 + 贪心 + 双指针
         *
         * dp[i]表示以array[i]为结尾(必选)的连续子数组的最大和
         *
         *         { dp[i-1] + array[i]  , dp[i-1] >= 0
         * dp[i] = {
         *         { array[i]            , dp[i-1] < 0
         *
         * @param array
         * @return
         */
        private int[] solution3(int[] array){
            int n = array.length;
            int[] dp = new int[n];
            dp[0] = array[0];
    
            // 连续子数组的最大和
            int sum = dp[0];
            // 当前区间
            int left = 0, right = 0;
            // 记录结果区间(和最大时的最长区间)
            int recLeft = 0, recRight = 0;
            for(int i=1; i<n; i++){
                right = i;
                // 贪心
                dp[i] = Math.max(dp[i-1]+array[i], array[i]);
                if(dp[i-1]+array[i] < array[i]){
                    left = right;
                }
                if(dp[i]>sum || (dp[i]==sum && right-left+1>recRight-recLeft+1)){
                    sum = dp[i];
                    recLeft = left;
                    recRight = right;
                }
            }
    
            int[] result = new int[recRight-recLeft+1];
            for(int i=recLeft; i<=recRight; i++){
                result[i-recLeft] = array[i];
            }
    
            return result;
        }
    
        /**
         * 动态规划(空间优化) + 贪心 + 双指针
         *
         * preSum 表示以数组中上一整数为结尾的连续子数组的最大和
         * curSum 表示以数组中当前整数为结尾的连续子数组的最大和
         *
         *          { preSum + array[i]  , preSum >= 0
         * curSum = {
         *          { array[i]           , preSum < 0
         *
         * @param array
         * @return
         */
        private int[] solution33(int[] array){
            int n = array.length;
    
            int curSum;
            int preSum = array[0];
    
            // 连续子数组的最大和
            int sum = array[0];
            // 当前区间
            int left = 0, right = 0;
            // 记录结果区间(和最大时的最长区间)
            int recLeft = 0, recRight = 0;
            for(int i=1; i<n; i++){
                right = i;
                // 贪心
                curSum = Math.max(preSum+array[i], array[i]);
                if(preSum+array[i] < array[i]){
                    left = right;
                }
                if(curSum>sum || (curSum==sum && right-left+1>recRight-recLeft+1)){
                    sum = curSum;
                    recLeft = left;
                    recRight = right;
                }
    
                preSum = curSum;
            }
    
            int[] result = new int[recRight-recLeft+1];
            for(int i=recLeft; i<=recRight; i++){
                result[i-recLeft] = array[i];
            }
    
            return result;
        }
    }
