# java-NC168 盛水最多的容器


    import java.util.*;
    
    /**
     * NC168 盛水最多的容器
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param height int整型一维数组
         * @return int整型
         */
        public int maxArea (int[] height) {
            return solution1(height);
            // return solution2(height);
        }
    
        /**
         * 双指针(对撞指针) + 贪心
         * @param height
         * @return
         */
        private int solution1(int[] height){
            int n = height.length;
            if(n < 2){
                return 0;
            }
    
            int result = 0;
            int water;
            int lower;
            // 双指针(对撞指针)
            int i=0,j=n-1;
            while(i < j){
                lower = Math.min(height[i],height[j]);
                water = lower*(j-i);
                result = Math.max(result, water);
                // 贪心
                if(height[i] <= height[j]){
                    while(i<j && height[i]<=lower){
                        i++;
                    }
                }else{
                    while(i<j && height[j]<=lower){
                        j--;
                    }
                }
            }
    
            return result;
        }
    
        /**
         * 双指针(对撞指针) + 贪心
         * @param height
         * @return
         */
        private int solution2(int[] height){
            int n = height.length;
            if(n < 2){
                return 0;
            }
    
            int result = 0;
            int water;
            int lower;
            // 双指针(对撞指针)
            int i=0,j=n-1;
            while(i < j){
                lower = Math.min(height[i],height[j]);
                water = lower*(j-i);
                result = Math.max(result, water);
                // 贪心
                if(height[i] <= height[j]){
                    i++;
                }else{
                    j--;
                }
            }
    
            return result;
        }
    }

  

