# java-NC413 两个升序数组的中位数


    import java.util.*;
    
    /**
     * NC413 两个升序数组的中位数
     * @author d3y1
     */
    public class Solution {
        private int n;
        private int m;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC36 在两个长度相等的排序数组中找到上中位数   [nowcoder]
         *
         * @param nums1 int整型ArrayList
         * @param nums2 int整型ArrayList
         * @return double浮点型
         */
        public double Median (ArrayList<Integer> nums1, ArrayList<Integer> nums2) {
            return solution1(nums1, nums2);
            // return solution2(nums1, nums2);
            // return solution3(nums1, nums2);
        }
    
        /**
         * 二分
         * @param nums1
         * @param nums2
         * @return
         */
        private double solution1(ArrayList<Integer> nums1, ArrayList<Integer> nums2){
            n = nums1.size();
            m = nums2.size();
    
            int k = (n+m)/2+1;
            // 奇数
            if((n+m)%2 == 1){
                return getKthNum(k, nums1, nums2);
            }
            // 偶数
            else{
                return (getKthNum(k-1, nums1, nums2)+getKthNum(k, nums1, nums2))/2.0;
            }
        }
    
        /**
         * 获取第K小的元素
         * @param k
         * @param nums1
         * @param nums2
         * @return
         */
        private int getKthNum(int k, ArrayList<Integer> nums1, ArrayList<Integer> nums2){
            int left1 = 0;
            int left2 = 0;
            int mid1,mid2;
            int half;
            while(true){
                if(left1 == n){
                    return nums2.get(left2+k-1);
                }
                if(left2 == m){
                    return nums1.get(left1+k-1);
                }
    
                if(k == 1){
                    return Math.min(nums1.get(left1), nums2.get(left2));
                }
    
                half = k/2-1;
                mid1 = (left1+half)<n ? left1+half : n-1;
                mid2 = (left2+half)<m ? left2+half : m-1;
    
                if(nums1.get(mid1) <= nums2.get(mid2)){
                    k -= (mid1-left1+1);
                    left1 = mid1+1;
                }else{
                    k -= (mid2-left2+1);
                    left2 = mid2+1;
                }
            }
        }
    
        /**
         * 二分
         * @param nums1
         * @param nums2
         * @return
         */
        private double solution2(ArrayList<Integer> nums1, ArrayList<Integer> nums2){
            n = nums1.size();
            m = nums2.size();
    
            if(n <= m){
                return divideArray(nums1, nums2);
            }else{
                return divideArray(nums2, nums1);
            }
        }
    
        /**
         * 划分数组
         * @param nums1
         * @param nums2
         * @return
         */
        private double divideArray(ArrayList<Integer> nums1, ArrayList<Integer> nums2){
            // 注意 n1<=n2 -> 确保j>=0
            int n1 = nums1.size();
            int n2 = nums2.size();
            int left = 0;
            int right = n1;
            int i,j;
            int nums1_i_1,nums1_i,nums2_j_1,nums2_j;
            int preMax=0,postMin=0;
            while(left <= right){
                // 前一部分包含 nums1[0 .. i-1] 和 nums2[0 .. j-1]
                // 后一部分包含 nums1[i .. n1-1] 和 nums2[j .. n2-1]
                i = (left+right)/2;
                j = (n1+n2+1)/2-i;
    
                nums1_i_1 = (i==0) ? Integer.MIN_VALUE : nums1.get(i-1);
                nums1_i = (i==n1) ? Integer.MAX_VALUE : nums1.get(i);
                nums2_j_1 = (j==0) ? Integer.MIN_VALUE : nums2.get(j-1);
                nums2_j = (j==n2) ? Integer.MAX_VALUE : nums2.get(j);
    
                if(nums1_i_1 <= nums2_j){
                    preMax = Math.max(nums1_i_1, nums2_j_1);
                    postMin = Math.min(nums1_i, nums2_j);
                    left = i+1;
                }else{
                    right = i-1;
                }
            }
    
            return (n1+n2)%2==1 ? preMax : (preMax+postMin)/2.0;
        }
    
        /**
         * 双指针
         * @param nums1
         * @param nums2
         * @return
         */
        private double solution3(ArrayList<Integer> nums1, ArrayList<Integer> nums2){
            n = nums1.size();
            m = nums2.size();
    
            int k = (n+m)/2+1;
    
            boolean isEven = (n+m)%2==0;
    
            int count = 0;
            double result = 0;
            int min;
            for(int i=0,j=0; i<n||j<m;){
                if(i == n){
                    min = nums2.get(j++);
                }else if(j == m){
                    min = nums1.get(i++);
                }else{
                    if(nums1.get(i) < nums2.get(j)){
                        min = nums1.get(i++);
                    }else{
                        min = nums2.get(j++);
                    }
                }
    
                count++;
    
                if(count == k-1){
                    if(isEven){
                        result += min;
                    }
                }
                if(count == k){
                    result += min;
                    if(isEven){
                        result /= 2.0;
                    }
                    break;
                }
            }
    
            return result;
        }
    }

  

