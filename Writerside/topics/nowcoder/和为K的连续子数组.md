# 和为K的连续子数组
https://www.nowcoder.com/practice/704c8388a82e42e58b7f5751ec943a11

    import java.util.*;
    
    /**
     * NC125 和为K的连续子数组
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * max length of the subarray sum = k
         * @param arr int整型一维数组 the array
         * @param k int整型 target
         * @return int整型
         */
        public int maxlenEqualK (int[] arr, int k) {
            // return solution1(arr, k);
            // return solution2(arr, k);
            // return solution3(arr, k);
            return solution33(arr, k);
        }
    
        /**
         * 枚举法: 超时!
         * @param arr
         * @param k
         * @return
         */
        private int solution1(int[] arr, int k){
            int n = arr.length;
            int result = 0;
            int sum;
            for(int j=0; j<n; j++){
                sum = 0;
                for(int i=j; i>=0; i--){
                    sum += arr[i];
                    if(sum == k){
                        result = Math.max(result, j-i+1);
                    }
                }
            }
    
            return result;
        }
    
        /**
         * 前缀和: 超时!
         * @param arr
         * @param k
         * @return
         */
        private int solution2(int[] arr, int k){
            int n = arr.length;
            int[] pre = new int[n+1];
            for(int i=1; i<=n; i++){
                pre[i] = pre[i-1]+arr[i-1];
            }
    
            int sum;
            for(int gap=n; gap>0; gap--){
                for(int i=0,j=i+gap; j<=n; i++,j++){
                    sum = pre[j]-pre[i];
                    if(sum == k){
                        return j-i;
                    }
                }
            }
    
            return 0;
        }
    
        /**
         * 前缀和 + 哈希
         * @param arr
         * @param k
         * @return
         */
        private int solution3(int[] arr, int k){
            int n = arr.length;
            int[] pre = new int[n+1];
            for(int i=1; i<=n; i++){
                pre[i] = pre[i-1]+arr[i-1];
            }
    
            int result = 0;
            HashMap<Integer,Integer> map = new HashMap<>();
            // sum=pre[j]-pre[i]=k => target=pre[i]=pre[j]-k
            int target;
            for(int j=0; j<=n; j++){
                target = pre[j]-k;
                if(map.containsKey(target)){
                    result = Math.max(result, j-map.get(target));
                }
                // 记录最左边即可(题目求解最长连续子数组长度)
                if(!map.containsKey(pre[j])){
                    // 表示: 前j个元素的和为pre[j]
                    map.put(pre[j], j);
                }
            }
    
            return result;
        }
    
        /**
         * 前缀和 + 哈希
         * 
         * 优化
         * 
         * @param arr
         * @param k
         * @return
         */
        private int solution33(int[] arr, int k){
            int n = arr.length;
            int result = 0;
            HashMap<Integer,Integer> map = new HashMap<>();
            // sum=pre[j]-pre[i]=k => target=pre[i]=pre[j]-k
            int target,pre=0;
            // 表示: 前0个元素的和为pre(0)
            map.put(pre, 0);
            for(int j=1; j<=n; j++){
                pre += arr[j-1];
                target = pre-k;
                if(map.containsKey(target)){
                    result = Math.max(result, j-map.get(target));
                }
                // 记录最左边即可(题目求解最长连续子数组长度)
                if(!map.containsKey(pre)){
                    // 表示: 前j个元素的和为pre
                    map.put(pre, j);
                }
            }
    
            return result;
        }
    }
    

