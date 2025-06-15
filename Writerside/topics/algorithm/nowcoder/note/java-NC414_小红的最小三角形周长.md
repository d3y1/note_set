# java-NC414 小红的最小三角形周长


    import java.util.*;
    
    /**
     * NC414 小红的最小三角形周长
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC254 合法的三角形个数 [nowcoder]
         *
         * @param nums int整型ArrayList
         * @return int整型
         */
        public int hongstriangle (ArrayList<Integer> nums) {
            // return solution1(nums);
            // return solution2(nums);
            return solution3(nums);
        }
    
        /**
         * 二分
         * @param nums
         * @return
         */
        private int solution1(ArrayList<Integer> nums){
            Collections.sort(nums);
    
            int n = nums.size();
            long result = Long.MAX_VALUE;
            long target;
            int left,right,mid,cnt;
            long sum;
            // 三角形两边之和大于第三边
            for(int i=0; i<n; i++){
                for(int j=i+1; j<n-1; j++){
                    // 当前最小的三边之和(可能不合法)
                    sum = (long) nums.get(i)+nums.get(j)+nums.get(j+1);
                    if(sum >= result){
                        break;
                    }
                    // 两条短边之和
                    target = (long) nums.get(i)+nums.get(j);
                    // 二分
                    left = j+1;
                    right = n-1;
                    while(left <= right){
                        mid = (left+right)/2;
                        if(nums.get(mid) < target){
                            left = mid+1;
                        }else{
                            right = mid-1;
                        }
                    }
    
                    // 可选第三边个数
                    cnt = (left-j-1);
                    if(cnt > 0){
                        result = sum;
                    }
                }
            }
    
            return (int)result;
        }
    
        /**
         * 双指针
         * @param nums
         * @return
         */
        private int solution2(ArrayList<Integer> nums){
            Collections.sort(nums);
    
            int n = nums.size();
            long result = Long.MAX_VALUE;
            long target;
            long sum;
            // 三角形两边之和大于第三边
            for(int i=0; i<n; i++){
                for(int j=i+1; j<n-1; j++){
                    // 当前最小的三边之和(可能不合法)
                    sum = (long) nums.get(i)+nums.get(j)+nums.get(j+1);
                    if(sum >= result){
                        break;
                    }
    
                    // 两条短边之和
                    target = (long) nums.get(i)+nums.get(j);
                    if(target > nums.get(j+1)){
                        result = sum;
                    }
                }
            }
    
            return (int)result;
        }
    
        /**
         * 二分
         * @param nums
         * @return
         */
        private int solution3(ArrayList<Integer> nums){
            Collections.sort(nums);
            int n = nums.size();
    
            int result = Integer.MAX_VALUE;
    
            int target;
            int left,right,mid;
            // 较大两边索引一定相邻(连续)!
            for(int i=2; i<n; i++){
                // A+B>C => A>C-B 第三条最小边大于target
                target = nums.get(i)-nums.get(i-1);
                left = 0;
                right = i-2;
                while(left <= right){
                    mid = left+(right-left)/2;
                    // left最终指向第一个大于target的位置
                    if(nums.get(mid) <= target){
                        left = mid+1;
                    }else{
                        right = mid-1;
                    }
                }
                if(left <= i-2){
                    result = Math.min(result, nums.get(left)+nums.get(i)+nums.get(i-1));
                }
            }
    
            return result;
        }
    }

  

