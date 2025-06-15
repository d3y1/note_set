# java-NC377 有序数组中出现一次的元素


    import java.util.*;
    
    /**
     * NC377 有序数组中出现一次的元素
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param v int整型一维数组
         * @return int整型
         */
        public int singleElement (ArrayList<Integer> v) {
    //        return solution1(v);
            return solution11(v);
    //        return solution2(v);
    //        return solution3(v);
    //        return solution4(v);
    //        return solution5(v);
        }
    
        /**
         * 二分
         * @param v
         * @return
         */
        private int solution1(ArrayList<Integer> v){
            int n = v.size();
    
            int result = -1;
    
            int left = 0;
            int right = n-1;
            int mid;
            int pre,after;
            while(left <= right){
                mid = left+(right-left)/2;
                if(mid%2 == 1){
                    pre = mid-1;
                    after = mid+1;
                    if(0<=pre && v.get(pre).equals(v.get(mid))){
                        left = mid+1;
                        continue;
                    }
                    if(after<n && v.get(mid).equals(v.get(after))){
                        right = mid-1;
                        continue;
                    }
                }
                // 最终结果一定是在 偶数索引位置
                else{
                    pre = mid-1;
                    after = mid+1;
    //                if(0<=pre && v.get(pre).equals(v.get(mid))){
    //                    right = mid-1;
    //                    continue;
    //                }
    //                if(after<n && v.get(mid).equals(v.get(after))){
    //                    left = mid+1;
    //                    continue;
    //                }
                    // 可减2
                    if(0<=pre && v.get(pre).equals(v.get(mid))){
                        right = mid-2;
                        continue;
                    }
                    // 可加2
                    if(after<n && v.get(mid).equals(v.get(after))){
                        left = mid+2;
                        continue;
                    }
                    // 前后 都不相同
                    result = v.get(mid);
                    break;
                }
            }
    
            return result;
        }
    
        /**
         * 二分
         * @param v
         * @return
         */
        private int solution11(ArrayList<Integer> v){
            int n = v.size();
    
            int result = -1;
    
            int left = 0;
            int right = n-1;
            int mid;
            int pre,after;
            while(left <= right){
                mid = left+(right-left)/2;
                if(mid%2 == 1){
                    pre = mid-1;
                    after = mid+1;
                    if(0<=pre && v.get(pre).equals(v.get(mid))){
                        left = mid+1;
                    }else if(after<n && v.get(mid).equals(v.get(after))){
                        right = mid-1;
                    }
                }else{
                    pre = mid-1;
                    after = mid+1;
                    if(0<=pre && v.get(pre).equals(v.get(mid))){
                        right = mid-2;
                    }else if(after<n && v.get(mid).equals(v.get(after))){
                        left = mid+2;
                    }else{
                        result = v.get(mid);
                        break;
                    }
                }
            }
    
            return result;
        }
    
        /**
         * 二分: 简化
         * @param v
         * @return
         */
        private int solution2(ArrayList<Integer> v){
            int n = v.size();
    
            int left = 0;
            int right = n-1;
            int mid;
            int pre,after;
            while(left < right){
                mid = left+(right-left)/2;
                if(mid%2 == 1){
                    pre = mid-1;
                    if(0<=pre && v.get(pre).equals(v.get(mid))){
                        left = mid+1;
                    }else{
                        right = mid;
                    }
                }else{
                    after = mid+1;
                    if(after<n && v.get(mid).equals(v.get(after))){
    //                    left = mid+1;
                        // 可加2
                        left = mid+2;
                    }else{
                        right = mid;
                    }
                }
            }
    
            return v.get(left);
        }
    
        /**
         * 二分: 再简化
         * @param v
         * @return
         */
        private int solution3(ArrayList<Integer> v){
            int n = v.size();
    
            int left = 0;
            int right = n-1;
            int mid;
            while(left < right){
                mid = left+(right-left)/2;
    
                if(v.get(mid).equals(v.get(mid^1))){
                    left = mid+1;
                }else{
                    right = mid;
                }
            }
    
            return v.get(left);
        }
    
        /**
         * 二进制: 位运算(异或^)
         * @param v
         * @return
         */
        private int solution4(ArrayList<Integer> v){
            int result = 0;
            for(int num: v){
                result ^= num;
            }
    
            return result;
        }
    
        /**
         * 遍历
         * @param v
         * @return
         */
        private int solution5(ArrayList<Integer> v){
            int n = v.size();
    
            int result = 0;
    
            for(int i=0; i<n; i+=2){
                if((i==n-1) || (!v.get(i).equals(v.get(i+1)))){
                    result = v.get(i);
                    break;
                }
            }
    
            return result;
        }
    }

  

